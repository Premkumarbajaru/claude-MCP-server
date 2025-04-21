Sure! Here's your GitHub `README.md` file, formatted and ready to copy and paste:

```markdown
# 🌦️ MCP Weather Server

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A production-ready MCP server that provides real-time weather data through Claude for Desktop.

---

## 🚀 Features

- ✅ **Real-time weather alerts** for any US state  
- ✅ **Detailed forecasts** by coordinates  
- ✅ **Simple MCP protocol** implementation  
- ✅ **Seamless integration** with Claude for Desktop  

---

## ⚡ Quick Start

### 📦 Prerequisites

- Python 3.10+
- [UV](https://github.com/astral-sh/uv) package manager
- Claude for Desktop (with MCP support)

---

### 🛠️ Installation

```bash
# Install UV
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# Set up project
uv init weather
cd weather
uv venv
.\.venv\Scripts\activate  # On Unix: source .venv/bin/activate
uv add mcp[cli] httpx
```

---

## 🧪 Server Implementation (`weather.py`)

```python
from typing import Any
import httpx
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("weather")
NWS_API_BASE = "https://api.weather.gov"
USER_AGENT = "weather-app/1.0"

async def make_nws_request(url: str) -> dict[str, Any] | None:
    async with httpx.AsyncClient() as client:
        response = await client.get(url, headers={"User-Agent": USER_AGENT})
        return response.json() if response.status_code == 200 else None

@mcp.tool()
async def get_alerts(state: str) -> str:
    url = f"{NWS_API_BASE}/alerts/active?area={state}"
    data = await make_nws_request(url)
    return "\n".join([alert["properties"]["headline"] for alert in data["features"]]) if data else "No alerts found"

@mcp.tool()
async def get_forecast(latitude: float, longitude: float) -> str:
    point_url = f"{NWS_API_BASE}/points/{latitude},{longitude}"
    point_data = await make_nws_request(point_url)
    forecast_url = point_data["properties"]["forecast"]
    forecast_data = await make_nws_request(forecast_url)
    return forecast_data["properties"]["periods"][0]["detailedForecast"] if forecast_data else "Forecast unavailable"

if __name__ == "__main__":
    mcp.run(transport='stdio')
```

---

## ⚙️ Configure Claude

Add this configuration to your `claude_desktop_config.json` file:

```json
{
  "mcpServers": {
    "weather": {
      "command": "uv",
      "args": [
        "--directory",
        "/path/to/weather",
        "run",
        "weather.py"
      ]
    }
  }
}
```

✅ Replace `/path/to/weather` with the absolute path to your project folder.

---

## 📚 API Reference

| Tool           | Parameters                               | Description                        |
|----------------|------------------------------------------|------------------------------------|
| `get_alerts`   | `state: str` (e.g., "CA")                | Returns active weather alerts      |
| `get_forecast` | `latitude: float`, `longitude: float`    | Returns detailed forecast          |

---

## 💬 Example Queries

- “What are the current weather alerts in Texas?”
- “What’s the forecast for New York City?”
- “Are there any severe weather warnings in California?”

---

## 🛠️ Troubleshooting

**Common Issues:**
- 📍 Make sure Claude config uses **absolute path**
- ⚙️ Confirm UV is available in system `PATH`
- 🌐 Check [NWS API](https://api.weather.gov) status
- 🧾 View server logs for runtime errors or failed requests

---

## 📜 License

MIT © 2023 Your Name
```

Let me know if you want to include a **Contributing** or **Acknowledgments** section, or if you're planning to publish this on PyPI or Docker—I'd be happy to tailor it further!
