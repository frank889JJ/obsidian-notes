# MCP Server Development Guide

## Overview

MCP (Model Context Protocol) servers extend AI assistants like Cline by providing capabilities to:

- Access external APIs and services
- Retrieve real-time data
- Control applications and local systems
- Perform actions beyond text prompts

## Development Protocol Structure

The protocol is implemented through a `.clinerules` file in your MCP working directory:

```bash
/Users/your-name/Documents/Cline/MCP/.clinerules
```

### Protocol Phases

1. **Planning (PLAN MODE)**
   - Problem definition
   - API/service selection
   - Authentication requirements

2. **Implementation (ACT MODE)**
   - Bootstrap setup
   - Core implementation
   - Configuration

3. **Testing (BLOCKER)**
   - Tool validation
   - Output verification
   - User confirmation

4. **Completion**
   - Final verification
   - Documentation
   - Deployment

## Current Configuration Analysis

From your current setup:

### MCP Servers Configuration (`cline_mcp_settings.json`):

```json
{
  "echo-server": {
    "command": "python",
    "args": ["/Users/linjunjie/Documents/学习项目/mcp/obsidian-mcp-cursor/src/server/server.py"]
  },
  "github": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-github"],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "..."
    }
  },
  "obsidian": {
    "command": "npx",
    "args": ["-y", "obsidian-mcp", "/Users/linjunjie/Documents/Obsidian"],
    "env": {
      "OBSIDIAN_API_KEY": "..."
    }
  }
}
```

### Extended MCP Configuration (`mcp.json`):

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "..."
      }
    },
    "fetch": {
      "command": ".../venv/bin/python",
      "args": ["-m", "mcp_server_fetch"],
      "env": {
        "PYTHONPATH": "/Users/linjunjie/Documents/学习项目/mcp"
      }
    },
    "hotnews": {
      "command": "npx",
      "args": ["-y", "@wopal/mcp-server-hotnews"],
      "env": {}
    },
    "puppeteer": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
    },
    "obsidian": {
      "command": "/opt/homebrew/bin/obsidian-mcp",
      "args": ["/Users/linjunjie/Documents/Obsidian/Vault"]
    },
    "server-sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@smithery/cli@latest",
        "run",
        "@smithery-ai/server-sequential-thinking",
        "--key",
        "..."
      ]
    }
  }
}
```

## Best Practices

### 1. Configuration Management

- Keep sensitive credentials in environment variables
- Use absolute paths for reliability
- Implement proper rate limiting
- Enable comprehensive logging

### 2. Development Workflow

1. Start with PLAN MODE
2. Document API requirements
3. Implement core functionality
4. Add comprehensive error handling
5. Test thoroughly
6. Document usage

### 3. Testing Requirements

- Test each tool individually
- Verify output formats
- Confirm user success
- Document test results

## Common Issues and Solutions

1. **Path Dependencies**
   - Use relative paths where possible
   - Verify file/directory existence
   - Handle path resolution errors

2. **Authentication**
   - Secure credential storage
   - Handle token expiration
   - Implement refresh mechanisms

3. **Rate Limiting**
   - Implement queuing
   - Add caching
   - Handle rate limit errors

## Resources

- [MCP Protocol Documentation](https://modelcontextprotocol.org/docs)
- [Cline Documentation](https://docs.cline.bot/)
- [MCP Server Examples](https://github.com/modelcontextprotocol/mcp-servers)