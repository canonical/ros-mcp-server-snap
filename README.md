# ros-mcp-server-snap

The [ROS MCP Server](https://github.com/robotmcp/ros-mcp-server) as a snap.

[![Get it from the Snap Store](https://snapcraft.io/en/dark/install.svg)](https://snapcraft.io/ros-mcp-server)
[![ros-mcp-server](https://snapcraft.io/ros-mcp-server/badge.svg)](https://snapcraft.io/ros-mcp-server)
[![ros-mcp-server](https://snapcraft.io/ros-mcp-server/trending.svg?name=0)](https://snapcraft.io/ros-mcp-server)

`ros-mcp-server` connects large language models (such as Claude, GPT, and Gemini)
to robots via the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/),
with no changes to existing robot source code.
It communicates with a running ROS system through a
[rosbridge](https://github.com/RobotWebTools/rosbridge_suite) WebSocket connection,
allowing LLMs to publish/subscribe to topics, call services and actions,
set parameters, and monitor robot state in real time.

Supports ROS 2 (Lyrical, Jazzy, Humble, and others) and ROS 1 distributions.

## Install

To install the snap from the store:

```bash
snap install ros-mcp-server
```

## Usage

### stdio transport (default)

The default transport is `stdio`, used when an MCP client (e.g. Claude Desktop)
launches the server as a subprocess:

```bash
ros-mcp-server
```

### HTTP transport

For network-accessible deployments, switch to the `http` or `streamable-http`
transport. When set, the snap automatically runs the server as a background
daemon that starts on boot and restarts on failure:

```bash
snap set ros-mcp-server transport=http
# or
snap set ros-mcp-server transport=streamable-http
```

To stop the daemon and revert to stdio:

```bash
snap set ros-mcp-server transport=stdio
```

## Configuration

All keys have defaults set at install time.

| Key | Default | Description |
|---|---|---|
| `transport` | `stdio` | Transport mode: `stdio`, `http`, or `streamable-http` |
| `host` | `127.0.0.1` | Bind address for HTTP transports |
| `port` | `9000` | Port for HTTP transports |

```bash
snap set ros-mcp-server transport=http host=0.0.0.0 port=9000
```

View the current configuration:

```bash
snap get ros-mcp-server
```

## Development

Make sure that snapcraft is [installed and set up](https://snapcraft.io/docs/snapcraft-setup).

To build the snap:

```bash
snapcraft pack
```

To install the locally built snap:

```bash
snap install --dangerous ros-mcp-server_*.snap
```
