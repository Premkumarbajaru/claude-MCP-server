

```markdown
# 🌦️ MCP Weather Server

A reliable MCP server providing real-time weather data integration with Claude for Desktop.

## ✨ Features

- Real-time NWS weather alerts by state
- 7-day forecasts by coordinates
- Lightweight MCP protocol implementation
- Claude for Desktop integration

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- UV package manager
- Claude for Desktop

### Installation

1. Install dependencies:
```bash
uv venv
.\.venv\Scripts\activate
```

2. Create `weather.py`:

## 🔌 Claude Integration

Add to `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "weather": {
      "command": "python",
      "args": ["weather.py"],
      "cwd": "/absolute/path/to/project"
    }
  }
}
```

## 📊 Example Usage

```plaintext
User: What's the weather in San Francisco?
Claude: [Uses get_forecast(37.7749, -122.4194)]
```
![Image](https://github.com/user-attachments/assets/96e97939-ae13-40a0-9c1e-a6863cac5d87)

![Image](https://github.com/user-attachments/assets/574fef9e-32ae-4110-b8b1-e4393565076d)

![Image](https://github.com/user-attachments/assets/916a1e83-5969-495b-a4e6-37b13beb2336)

## 🛠 Troubleshooting

| Issue | Solution |
|-------|----------|
| Connection failed | Verify Claude's config path is absolute |
| No weather data | Check NWS API status at api.weather.gov |
| Module errors | Run `uv add mcp[cli] httpx` |
