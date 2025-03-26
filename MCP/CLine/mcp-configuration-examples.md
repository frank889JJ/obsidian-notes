# MCP Configuration Examples

## Basic Server Configuration

### TypeScript/Node.js Project

```json
{
  "mcpServers": {
    "my-server": {
      "command": "node",
      "args": ["path/to/build/index.js"],
      "env": {
        "API_KEY": "your-api-key"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

### Python Project

```json
{
  "mcpServers": {
    "my-server": {
      "command": "python",
      "args": ["server.py"],
      "env": {
        "API_KEY": "your-api-key",
        "PYTHONPATH": "/path/to/project"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Your Current Configuration Analysis

### Main Configuration (`cline_mcp_settings.json`)

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

### Extended Configuration (`mcp.json`)

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

## Configuration Best Practices

1. **Security**
   - Never commit API keys or tokens
   - Use environment variables for sensitive data
   - Implement proper access controls

2. **Path Management**
   - Use absolute paths for critical files
   - Verify file existence before execution
   - Handle path resolution errors

3. **Server Management**
   - Enable logging for debugging
   - Implement proper error handling
   - Use rate limiting where needed
   - Configure appropriate timeouts

4. **Environment Variables**
   - Use descriptive names
   - Document required variables
   - Provide example configurations
   - Validate environment variables on startup

## Common Configuration Patterns

### API Server

```json
{
  "mcpServers": {
    "api-server": {
      "command": "node",
      "args": ["api-server.js"],
      "env": {
        "API_KEY": "key",
        "API_URL": "https://api.example.com",
        "RATE_LIMIT": "100"
      }
    }
  }
}
```

### Database Server

```json
{
  "mcpServers": {
    "db-server": {
      "command": "python",
      "args": ["db_server.py"],
      "env": {
        "DB_HOST": "localhost",
        "DB_PORT": "5432",
        "DB_USER": "user",
        "DB_PASSWORD": "password"
      }
    }
  }
}
```

### File System Server

```json
{
  "mcpServers": {
    "fs-server": {
      "command": "node",
      "args": ["fs-server.js"],
      "env": {
        "ROOT_DIR": "/path/to/files",
        "MAX_FILE_SIZE": "10mb"
      }
    }
  }
}
```

## Troubleshooting

1. **Server Won't Start**
   - Check file paths
   - Verify environment variables
   - Check permissions
   - Review logs

2. **Authentication Errors**
   - Verify API keys/tokens
   - Check environment variables
   - Confirm proper formatting

3. **Path Resolution Issues**
   - Use absolute paths
   - Check file permissions
   - Verify directory structure