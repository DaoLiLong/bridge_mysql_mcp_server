
# MySQL MCP Server
A Model Context Protocol (MCP) implementation that enables secure interaction with MySQL databases. This server component facilitates communication between AI applications (hosts/clients) and MySQL databases, making database exploration and analysis safer and more structured through a controlled interface.

> **Note**: MySQL MCP Server is not designed to be used as a standalone server, but rather as a communication protocol implementation between AI applications and MySQL databases.

## Features
- List available MySQL tables as resources
- Read table contents
- Execute SQL queries with proper error handling
- Secure database access through environment variables
- Comprehensive logging


## Configuration
Set the following environment variables:
```bash
MYSQL_HOST=localhost     # Database host
MYSQL_PORT=3306         # Optional: Database port (defaults to 3306 if not specified)
MYSQL_USER=your_username
MYSQL_PASSWORD=your_password
MYSQL_DATABASE=your_database
```

## Usage
### With Claude Desktop
Add this to your `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "mysql": {
      "command": "uv",
      "args": [
        "--directory",
        "path/to/mysql_mcp_server",
        "run",
        "mysql_mcp_server"
      ],
      "env": {
        "MYSQL_HOST": "localhost",
        "MYSQL_PORT": "3306",
        "MYSQL_USER": "your_username",
        "MYSQL_PASSWORD": "your_password",
        "MYSQL_DATABASE": "your_database"
      }
    }
  }
}
```

### With Visual Studio Code
Add this to your `mcp.json`:
```json
{
  "servers": {
      "mysql": {
            "type": "stdio",
            "command": "uvx",
            "args": [
                "--from",
                "mysql-mcp-server",
                "mysql_mcp_server"
            ],
      "env": {
        "MYSQL_HOST": "localhost",
        "MYSQL_PORT": "3306",
        "MYSQL_USER": "your_username",
        "MYSQL_PASSWORD": "your_password",
        "MYSQL_DATABASE": "your_database"
      }
    }
  }
}
```
Note: Will need to install uv for this to work

### Debugging with MCP Inspector
While MySQL MCP Server isn't intended to be run standalone or directly from the command line with Python, you can use the MCP Inspector to debug it.

The MCP Inspector provides a convenient way to test and debug your MCP implementation:

```bash
# Install dependencies
pip install -r requirements.txt
# Use the MCP Inspector for debugging (do not run directly with Python)
```

The MySQL MCP Server is designed to be integrated with AI applications like Claude Desktop and should not be run directly as a standalone Python program.

## Development
```bash
# Clone the repository
git clone https://github.com/DaoLiLong/bridge_mysql_mcp_server.git
cd mysql_mcp_server
# Create virtual environment
python -m venv venv
source venv/bin/activate  # or `venv\Scripts\activate` on Windows
# Install development dependencies
pip install -r requirements-dev.txt
# Run tests
pytest
```

## windows版
# 创建虚拟环境目录
python -m venv .venv

# 使用当前项目下 .venv 虚拟环境中的 pip 工具，从阿里云的镜像源下载并安装 requirements.txt 文件中列出的所有依赖包。
.\.venv\Scripts\pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple


## mac版
# 创建虚拟环境目录
python -m venv .venv

# 激活当前目录下的 Python 虚拟环境
source .venv/bin/activate  

# 使用当前项目下 .venv 虚拟环境中的 pip 工具，从阿里云的镜像源下载并安装 requirements.txt 文件中列出的所有依赖包。
./.venv/bin/pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple


## 创建MCP MySQL连接
# 命令 windows版	
BridgeMysqlMcpServer的python项目地址\.venv\Scripts\python.exe
# 命令 mac版	
BridgeMysqlMcpServer的python项目地址/.venv/bin/python

# 参数 windows版	
BridgeMysqlMcpServer的python项目地址\src\mysql_mcp_server\server.py --transport stdio
# 参数 mac版	
BridgeMysqlMcpServer的python项目地址/server.py --transport stdio




## Security Considerations
- Never commit environment variables or credentials
- Use a database user with minimal required permissions
- Consider implementing query whitelisting for production use
- Monitor and log all database operations

## Security Best Practices
This MCP implementation requires database access to function. For security:
1. **Create a dedicated MySQL user** with minimal permissions
2. **Never use root credentials** or administrative accounts
3. **Restrict database access** to only necessary operations
4. **Enable logging** for audit purposes
5. **Regular security reviews** of database access
