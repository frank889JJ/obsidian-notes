# MCP Server Development Protocol

⚠️ **重要提示**: 在测试之前不要使用 attempt_completion ⚠️

## 第一步：规划 (PLAN MODE)
- 这个工具解决什么问题？
- 使用什么 API/服务？
- 认证要求是什么？
  □ 标准 API key
  □ OAuth (需要单独的设置脚本)
  □ 其他凭证

## 第二步：实现 (ACT MODE)

### 1. 引导设置

对于 Web 服务、JavaScript 集成或 Node.js 环境：
```bash
npx @modelcontextprotocol/create-server my-server
cd my-server
npm install
```

对于数据科学、ML 工作流或 Python 环境：
```bash
pip install mcp
# 或使用 uv (推荐)
uv add "mcp[cli]"
```

### 2. 核心实现
- 使用 MCP SDK
- 实现全面的日志记录
  
  TypeScript (Web/JS 项目):
  ```typescript
  console.error('[Setup] Initializing server...');
  console.error('[API] Request to endpoint:', endpoint);
  console.error('[Error] Failed with:', error);
  ```
  
  Python (数据科学/ML 项目):
  ```python
  import logging
  logging.error('[Setup] Initializing server...')
  logging.error(f'[API] Request to endpoint: {endpoint}')
  logging.error(f'[Error] Failed with: {str(error)}')
  ```
- 添加类型定义
- 处理带上下文的错误
- 如需要实现速率限制

### 3. 配置
- 如需要从用户获取凭证
- 添加到 MCP 设置：
  
  TypeScript 项目:
  ```json
  {
    "mcpServers": {
      "my-server": {
        "command": "node",
        "args": ["path/to/build/index.js"],
        "env": {
          "API_KEY": "key"
        },
        "disabled": false,
        "autoApprove": []
      }
    }
  }
  ```
  
  Python 项目:
  ```bash
  # 直接使用命令行
  mcp install server.py -v API_KEY=key
  
  # 或在 settings.json 中
  {
    "mcpServers": {
      "my-server": {
        "command": "python",
        "args": ["server.py"],
        "env": {
          "API_KEY": "key"
        },
        "disabled": false,
        "autoApprove": []
      }
    }
  }
  ```

## 第三步：测试 (阻塞步骤 ⛔️)

<思考>在使用 attempt_completion 之前，我必须验证：
□ 是否已测试每个工具？
□ 是否已确认用户对每个测试的成功？
□ 是否已记录测试结果？

如果有任何一个答案是"否"，我必须不能使用 attempt_completion。</思考>

1. 测试每个工具（必需）
   □ 使用有效输入测试每个工具
   □ 验证输出格式是否正确
   ⚠️ 在所有工具测试完成之前不要继续

## 第四步：完成

❗ 停止并验证：
□ 每个工具都已用有效输入测试
□ 每个工具的输出格式都正确

只有在所有工具都经过测试后才能使用 attempt_completion。

## 关键要求
- ✓ 必须使用 MCP SDK
- ✓ 必须有全面的日志记录
- ✓ 必须单独测试每个工具
- ✓ 必须优雅地处理错误
- ⛔️ 在完成前绝不能跳过测试