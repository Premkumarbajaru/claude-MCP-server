
```markdown
# 🌦️ MCP Weather Server

A production-ready MCP server that provides real-time weather data through Claude for Desktop.

---

## 🚀 Features

- ✅ Real-time weather alerts for any US state  
- ✅ Detailed forecasts by coordinates  
- ✅ Simple MCP protocol implementation  
- ✅ Seamless integration with Claude for Desktop  

---

## ⚡ Quick Start

### 📦 Prerequisites

- Python 3.10+
- [UV](https://modelcontextprotocol.io/quickstart/server) package manager
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
.\.venv\Scripts\activate
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
![Image](https://github.com/user-attachments/assets/96e97939-ae13-40a0-9c1e-a6863cac5d87)

---

![Image](https://github.com/user-attachments/assets/574fef9e-32ae-4110-b8b1-e4393565076d)

---

![Image](https://github.com/user-attachments/assets/916a1e83-5969-495b-a4e6-37b13beb2336)

---

## 🛠️ Troubleshooting

**Common Issues:**
- 📍 Make sure Claude config uses **absolute path**
- ⚙️ Confirm UV is available in system `PATH`
- 🧾 View server logs for runtime errors or failed requests
