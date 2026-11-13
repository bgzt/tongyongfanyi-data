# tongyongfanyi-data

《通用翻译》Minecraft 模组的远程数据表，供模组在启动时自动检查更新。

| 文件 | 内容 | 条数 |
|---|---|---|
| `item_names.json` | Hypixel SkyBlock NEU 仓库物品名 → 简体中文 | 7012 |
| `glossary.json` | 游戏术语固定译名 | 3374 |
| `manifest.json` | 版本号、条数、sha256（模组据此判断要不要下载） | — |

格式均为扁平 JSON：`{"英文原文小写": "中文译文"}`。

模组按以下顺序尝试下载（前一个失败自动换下一个）：
`raw.githubusercontent.com` → `api.github.com` → `cdn.jsdelivr.net` → `raw.gitmirror.com`。
全部失败时回退到 jar 内置的那份表。

> 更新数据后，请同时把 `manifest.json` 里对应表的 `version` 加 1、更新 `count` 与 `sha256`，
> 否则客户端不会重新下载。
