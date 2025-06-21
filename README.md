# ClickUp MCP Server

A Model Context Protocol (MCP) server that enables AI assistants to interact with ClickUp's task management API. This server provides core task management capabilities through natural language, focusing on essential project workflows rather than ClickUp's full feature set.

Built by the [Diversio](https://diversio.com) team for streamlined AI-powered task management.

<a href="https://glama.ai/mcp/servers/@DiversioTeam/clickup-mcp">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@DiversioTeam/clickup-mcp/badge" alt="ClickUp Server MCP server" />
</a>

## 🚀 What This Server Provides

### ✅ Core Task Management
- **Task CRUD Operations** - Create, read, update, and delete tasks
- **Task Organization** - Navigate spaces, folders, and lists
- **Task Search & Filtering** - Find tasks by various criteria
- **Assignee Management** - Assign users and check assignments
- **Status Management** - Update and track task statuses

### ✅ Productivity Features
- **Bulk Operations** - Update or move multiple tasks at once
- **Time Tracking** - Log time and view tracked hours
- **Task Templates** - Create tasks from predefined templates (bug report, feature request, code review)
- **Task Chains** - Create sequences of dependent tasks
- **Team Analytics** - View workload distribution and completion metrics

### ✅ Flexible ID Support
- Standard ClickUp IDs (`abc123`)
- Custom ID patterns (`gh-123`, `bug-456`)
- ClickUp URLs (`https://app.clickup.com/t/abc123`)
- Hash format (`#123`)

### ❌ What's NOT Included

This server focuses on task management essentials. **Not supported:**
- ClickUp Docs/Documents
- Whiteboards
- Dashboards
- Automations/Workflows
- Goals/Targets
- File/Attachment management
- Webhook management
- Advanced custom field operations
- Calendar views
- Forms integration

**API Coverage:** ~30-40% of ClickUp's full API, covering the most common task management workflows.

## Installation

### Quick Start (Recommended)

```bash
# Install from GitHub (latest)
uvx --from git+https://github.com/DiversioTeam/clickup-mcp clickup-mcp

# Or from PyPI (when published)
uvx clickup-mcp
```

### Development Installation

```bash
git clone https://github.com/DiversioTeam/clickup-mcp
cd clickup-mcp
uv sync
uv run clickup-mcp
```

## Configuration

### API Key Setup

```bash
# Set your ClickUp API key
uvx clickup-mcp set-api-key YOUR_API_KEY_HERE

# Or set environment variable
export CLICKUP_MCP_API_KEY=your_api_key
```

### Getting Your ClickUp API Key

**Step-by-step instructions:**

1. **Log in to ClickUp** at [https://app.clickup.com](https://app.clickup.com)
2. **Navigate to Settings**:
   - Click your avatar/profile picture in the bottom left corner
   - Select "Settings" from the dropdown menu
3. **Go to Apps section**:
   - In the left sidebar, click "Apps"
   - Then click "API" (or go directly to [https://app.clickup.com/settings/apps](https://app.clickup.com/settings/apps))
4. **Generate API Token**:
   - Click the "Generate" button to create a new personal API token
   - **Important**: This token will only be shown once!
5. **Copy and Save**:
   - Copy the generated token immediately
   - Store it securely (password manager recommended)
   - Configure it using: `uvx clickup-mcp set-api-key YOUR_TOKEN_HERE`

**Important Notes:**
- Personal API tokens have the same permissions as your user account
- Keep your token secure - treat it like a password
- If you lose the token, you'll need to regenerate a new one
- Tokens don't expire but can be revoked in the same settings page

## Usage with AI Assistants

### Claude Code (CLI)

Add to `~/.config/claude-code/mcp-settings.json`:

```json
{
  "servers": {
    "clickup": {
      "command": "uvx",
      "args": ["--from", "git+https://github.com/DiversioTeam/clickup-mcp.git", "clickup-mcp"]
    }
  }
}
```

### Claude Desktop

Add to your Claude Desktop config file:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
**Linux**: `~/.config/claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "clickup": {
      "command": "uvx",
      "args": ["--from", "git+https://github.com/DiversioTeam/clickup-mcp.git", "clickup-mcp"]
    }
  }
}
```

### VS Code

VS Code has excellent MCP support through both native integration and extensions. Multiple setup options available:

#### Option 1: Native VS Code MCP (Recommended)

VS Code now has built-in MCP support with GitHub Copilot and Agent Mode. Add to your workspace:

**Create `.vscode/mcp.json` in your project:**

```json
{
  "servers": {
    "clickup": {
      "command": "uvx",
      "args": ["--from", "git+https://github.com/DiversioTeam/clickup-mcp.git", "clickup-mcp"]
    }
  }
}
```

**Or add to VS Code User Settings:**

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run "Preferences: Open User Settings (JSON)"
3. Add to settings:

```json
{
  "mcp": {
    "servers": {
      "clickup": {
        "command": "uvx",
        "args": ["--from", "git+https://github.com/DiversioTeam/clickup-mcp.git", "clickup-mcp"]
      }
    }
  }
}
```

#### Option 2: VS Code Extensions with MCP Support

**Copilot MCP Extension:**
1. Install "Copilot MCP" from VS Code Marketplace
2. Search, manage, and install MCP servers directly from VS Code
3. The extension will help you configure the ClickUp MCP server

**Cline (AI Coding Assistant):**
1. Install "Cline" extension for advanced AI coding with MCP support
2. Configure ClickUp MCP server through Cline's settings

#### Managing MCP Servers in VS Code

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run **"MCP: List Servers"** to view configured servers
3. Select ClickUp server to **Start/Stop/Restart** or view logs
4. Use **"MCP: Show Output"** for debugging

#### Verify VS Code Setup

1. Ensure your ClickUp API key is configured: `uvx clickup-mcp set-api-key YOUR_KEY`
2. In VS Code, ask GitHub Copilot: *"Can you list my ClickUp spaces using MCP tools?"*
3. Check MCP server status with Command Palette → **"MCP: List Servers"**

## Available Tools (24 Tools)

### 📝 Task Management
- `create_task` - Create new tasks
- `get_task` - Get task details (supports various ID formats)
- `update_task` - Update task properties
- `delete_task` - Delete tasks
- `create_task_from_template` - Create from predefined templates
- `create_task_chain` - Create dependent task sequences

### 🔍 Task Discovery
- `list_tasks` - List tasks with filtering options
- `search_tasks` - Search tasks by text and criteria
- `get_subtasks` - Get all subtasks of a parent
- `get_task_comments` - Get comments on tasks

### 👥 Assignment & Status
- `get_task_status` - Get current task status
- `update_task_status` - Change task status
- `get_assignees` - List task assignees
- `assign_task` - Assign users to tasks

### 🗂️ Navigation
- `list_spaces` - List all spaces in workspace
- `list_folders` - List folders in a space
- `list_lists` - List all lists
- `find_list_by_name` - Find lists by name

### ⚡ Bulk Operations
- `bulk_update_tasks` - Update multiple tasks at once
- `bulk_move_tasks` - Move multiple tasks to different lists

### ⏱️ Time Tracking
- `get_time_tracked` - Get time tracked for users/periods
- `log_time` - Log time spent on tasks

### 📊 Analytics
- `get_team_workload` - See task distribution across team members
- `get_task_analytics` - Get velocity metrics and completion rates

## Example Usage

### Natural Language Commands

Ask your AI assistant:

```
"Create a bug report for login issues in the Development list"
"Show me all high-priority tasks assigned to me"
"Move all completed tasks from Sprint 1 to Archive"
"Log 2 hours on task gh-123 for debugging"
"What's our team's current workload?"
"Create a task chain: Design → Implement → Test → Deploy"
```

### Task Templates

```
"Create a bug report template for the payment processing issue"
"Use the code review template for PR #456"
"Create a feature request for dark mode"
```

### Analytics Queries

```
"What's our task completion rate this month?"
"Who has the most tasks assigned?"
"Show me time tracked on the API project"
```

## Development

### Running Tests

```bash
# Run all tests (48 tests)
uv run pytest

# Run with coverage
uv run pytest --cov=clickup_mcp

# Run specific test
uv run pytest tests/test_client.py::test_create_task
```

### Code Quality

```bash
# Check code style
uv run ruff check .

# Format code
uv run ruff format .

# Type checking
uv run mypy src/
```

## Troubleshooting

### Check Configuration

```bash
# Verify API key is configured
uv run clickup-mcp check-config

# Test API connection
uv run clickup-mcp test-connection
```

### Debug Mode

```bash
# Run with debug logging
uv run clickup-mcp --debug
```

## Technical Limitations

- **Rate Limiting**: No built-in rate limiting (ClickUp: 100 req/min)
- **Pagination**: Limited pagination support
- **Caching**: No response caching implemented
- **Custom Fields**: Models exist but limited tool support
- **Error Recovery**: Basic error handling without sophisticated retry

## Contributing

We welcome contributions! Focus areas:

### Priority Improvements
- Enhanced error handling and retry logic
- Response caching implementation
- Better pagination support
- Expanded custom field support

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Make changes and add tests
4. Ensure all tests pass (`uv run pytest`)
5. Run linting (`uv run ruff check .`)
6. Submit a Pull Request

### Development Setup

```bash
git clone https://github.com/yourusername/clickup-mcp
cd clickup-mcp
uv sync
uv run pytest  # Ensure tests pass
```

## Support

- **Issues**: [GitHub Issues](https://github.com/DiversioTeam/clickup-mcp/issues)
- **Discussions**: [GitHub Discussions](https://github.com/DiversioTeam/clickup-mcp/discussions)
- **Email**: tech@diversio.com

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built by [Diversio](https://diversio.com) team
- Powered by [Model Context Protocol](https://modelcontextprotocol.io)
- Uses [ClickUp API v2](https://clickup.com/api)