# Weather MCP Server

一个基于 [HelloAgents](https://github.com/HelloAgentsInc/hello-agents) 框架的实时天气查询 MCP Server。服务通过 HTTP transport 暴露 MCP 接口，并使用 `wttr.in` 获取当前天气数据。

## 功能

- 查询指定城市的实时天气
- 返回温度、体感温度、湿度、天气状况、风速、能见度和查询时间
- 支持常见中文城市名映射
- 提供服务器信息查询工具
- 支持 Docker 和 Smithery 部署

## 工具列表

### `get_weather`

获取指定城市的当前天气。

参数：

| 名称 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `city` | `string` | 是 | 城市名称，支持中文城市名或英文城市名 |

示例返回：

```json
{
  "city": "北京",
  "temperature": 22,
  "feels_like": 23,
  "humidity": 45,
  "condition": "Partly cloudy",
  "wind_speed": 3.6,
  "visibility": 10,
  "timestamp": "2026-05-03 16:30:00"
}
```

### `list_supported_cities`

列出内置支持的中文城市。

当前包含：北京、上海、广州、深圳、杭州、成都、重庆、武汉、西安、南京、天津、苏州。

### `get_server_info`

获取服务器名称、版本和可用工具列表。

## 环境要求

- Python 3.10+
- `hello-agents>=0.2.2`
- `requests>=2.31.0`

## 本地运行

1. 安装依赖：

```bash
pip install -r requirements.txt
```

2. 启动服务：

```bash
python server.py
```

默认服务地址：

```text
http://0.0.0.0:8081/mcp
```

可以通过环境变量修改监听地址和端口：

```bash
HOST=127.0.0.1 PORT=8081 python server.py
```

在 Windows PowerShell 中：

```powershell
$env:HOST = "127.0.0.1"
$env:PORT = "8081"
python server.py
```

## Docker 运行

构建镜像：

```bash
docker build -t weather-mcp-server .
```

启动容器：

```bash
docker run --rm -p 8081:8081 weather-mcp-server
```

服务端点：

```text
http://localhost:8081/mcp
```

## Smithery 部署

本项目已经包含 `smithery.yaml` 和 `Dockerfile`，可用于提交到 Smithery。

提交前请确认：

- `README.md` 和 `LICENSE` 已存在
- `pyproject.toml`、`smithery.yaml` 和 `Dockerfile` 配置正确
- 服务可以在本地正常启动
- GitHub 仓库为公开仓库

## 项目结构

```text
.
├── Dockerfile
├── LICENSE
├── PUBLISH_CHECKLIST.md
├── README.md
├── pyproject.toml
├── requirements.txt
├── server.py
└── smithery.yaml
```

## 数据来源

天气数据来自 [wttr.in](https://wttr.in/)。

## 许可证

本项目基于 MIT License 开源，详见 [LICENSE](LICENSE)。
