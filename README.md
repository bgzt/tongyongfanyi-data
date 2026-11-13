# tongyongfanyi-data

《通用翻译》Minecraft 模组的远程数据表。

**只在玩家手动触发时拉取**：模组启动、进游戏、切界面都不会发任何网络请求。
玩家在「设置 → SkyBlock 翻译增强 → 检查并更新数据表」点一下（或输入 `/tyfy tables`），
模组才会读 `manifest.json`、比对版本并下载新版表。不点就一直用当前表
（已下载过的表，或 jar 内置的那份打版快照）。

| 文件 | 内容 | 条数 |
|---|---|---|
| `item_names.json` | Hypixel SkyBlock NEU 仓库物品名 → 简体中文 | 7012 |
| `glossary.json` | 游戏术语固定译名 | 3374 |
| `manifest.json` | 版本号、条数、sha256（模组据此判断要不要下载） | — |

格式均为扁平 JSON：`{"英文原文小写": "中文译文"}`。

模组按以下顺序尝试下载（前一个失败自动换下一个，成功的源会被记住、下次优先用）：
`api.github.com/repos/.../contents` → `raw.githubusercontent.com` → `cdn.jsdelivr.net`
→ `raw.gitmirror.com` → `gh-proxy.com`。
国内网络下 `raw.githubusercontent.com` 常 TLS 握手失败，`api.github.com` 通常可直连，所以 API 排第一。
全部失败时什么都不做：继续用本地表，没有就用 jar 内置的那份。

下载的表落在 `config/tongyongfanyi/tables/`，校验 sha256 后原子替换，
随后在主线程重建术语表，本次游戏内立即生效。

> 更新数据后，请同时把 `manifest.json` 里对应表的 `version` 加 1、更新 `count` / `size` / `sha256`，
> 否则玩家点更新时会得到「已是最新」而不会重新下载。
