# floria-card-models

Floria 工作区预览卡片「模型」——在 Floria 预览面板里查看凭据池中的模型清单与端点，并为某个 provider 配置密钥。

## 功能

- 读取网关凭据池，按 provider 分组列出模型与端点
- 直接写入模型配置（新增 / 切换默认模型 / 保存密钥）
- 单文件、零构建、无外部依赖（图标为内联 SVG）

## 数据接口

卡片运行在 Floria 预览宿主内时，通过同源网关接口取数：

| 接口 | 用途 |
|---|---|
| `GET /gateway/models` | 模型与 provider 清单 |
| `GET /gateway/file?label=&path=` | 读取模型配置文件 |
| `POST /gateway/file/create` / `POST /gateway/file/write` | 新建 / 写入配置 |
| `?token=<网关 token>` | 非浏览器授权场景下的鉴权参数 |

页面 URL 上的 `token` 查询参数会被自动拼到后续请求上。

## 使用

把 `index.html` 放到工作区的 `<工作区>/.claude/preview/models/index.html`，并在同级 `preview.json` 里注册：

```json
{
  "id": "models",
  "title": "模型",
  "icon": "chip",
  "host": "view",
  "path": "models/index.html"
}
```

也可以直接用浏览器打开 `index.html` 查看静态界面——但此时没有网关，数据接口不可用。
