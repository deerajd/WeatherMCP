# MCP Weather Server

A Model Context Protocol (MCP) server that enables LLM-based AI agents to access real-time weather information. Designed for seamless integration with LLMs and AI agents using the MCP protocol and the National Weather Service API.

---

## Features

- Exposes weather-related tools for LLM agents via MCP:
  - `get_forecast`: Get detailed weather forecasts by latitude/longitude
  - `get_alerts`: Get active weather alerts by US state
- Uses the National Weather Service (NWS) API for accurate, up-to-date weather data
- Asynchronous HTTP requests for non-blocking performance
- Simple integration with Claude, MCP clients, or other LLM-based agents
- US-only coverage (National Weather Service limitation)

---

## Quickstart

### 1. Install & Run

Run the MCP Weather Server using [`uvx`](https://github.com/uvx-dev/uvx):

```bash
uvx --from git+https://github.com/deerajd/WeatherMCP.git mcp-server
```

---

### 2. Integrate with Your LLM Agent

Add the following to your tool configuration (for Claude, MCP clients, etc.):

```json
{
  "mcpServers": {
    "Weather": {
      "command": "uvx",
      "args": [
        "--from",
        "git+https://github.com/deerajd/WeatherMCP.git",
        "mcp-server"
      ]
    }
  }
}
```

This configuration launches the MCP Weather Server as a subprocess, exposing weather tools to your LLM agent.

---

### 3. Usage

From your LLM agent, you can call:

#### Get Weather Forecast
```
get_forecast(latitude=40.7128, longitude=-74.0060)  # New York City
```

#### Get Weather Alerts
```
get_alerts(state="NY")  # New York state alerts
```

The server will respond with detailed weather information including:
- Temperature, wind conditions, and detailed forecasts
- Active weather alerts with severity levels and instructions
- Multi-day forecast periods

---

## API Reference

### `get_forecast(latitude, longitude)`
- **Parameters:**
  - `latitude` (float): Latitude of the location
  - `longitude` (float): Longitude of the location
- **Returns:** Detailed weather forecast for the next 5 periods
- **Coverage:** US locations only

### `get_alerts(state)`
- **Parameters:**
  - `state` (str): Two-letter US state code (e.g., "CA", "NY", "TX")
- **Returns:** Active weather alerts for the specified state
- **Coverage:** US states only

---

## Development

- Python 3.8+
- [`httpx`](https://pypi.org/project/httpx/) for async HTTP requests
- [`FastMCP`](https://github.com/modelcontext/fastmcp) for MCP server implementation
- National Weather Service API

---

## License

MIT License

---
