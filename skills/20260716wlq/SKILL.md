---
name: html-poster-generator
description: 把榜单 / 排名表 / Top-N 清单 / 书单歌单等数据生成可分享的高清海报图片（PNG）。当用户给出一张排名表、列表并说“出图 / 做个图 / 生成海报 / 来张图”时使用。用 HTML+CSS 排版，再通过 Microsoft Edge 无头模式截图成 PNG，避免 AI 文生图导致的中文乱码。
agent_created: true
---

# HTML 海报生成器

## 何时用
- 用户输入一张排名表 / 清单 / Top-N（含中文书名、台词、标签等），要求“出图”“生成海报”。
- 需要清晰中文、可二次修改、批量产出多种版式。
- **不要用 AI 文生图**：榜单里有大量中文专名与台词，文生图极易乱码。HTML 排版 + 浏览器截图是稳的输出方式。

## 工作流
1. 把数据写成一个自包含 HTML（CSS 内联，不依赖外部资源），存到当前工作目录。
2. 用 Microsoft Edge 无头模式把 HTML 截图成 PNG。
3. 校验：用 Read 工具打开 PNG 看是否有截断 / 乱码，必要时调高度重截。
4. present_files 交付，并保留同名 .html 源文件以便二次修改。

## 截图命令（Windows，本机可用）
Edge 路径：`C:/Program Files (x86)/Microsoft/Edge/Application/msedge.exe`
```bash
EDGE="/c/Program Files (x86)/Microsoft/Edge/Application/msedge.exe"
D="C:/Users/72689/WorkBuddy/<日期目录>"
"$EDGE" --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --force-device-scale-factor=1 --window-size=1080,2160 \
  --screenshot="$D/out.png" "file://$D/out.html"
```
- `--window-size=W,H` 的 H 必须等于或超过页面真实高度，否则**底部内容被截断**（见下方坑点）。
- `--force-device-scale-factor=1` 保证 1:1 像素，输出尺寸 = window-size。

## 可用中文字体（C:\Windows\Fonts）
在 CSS `font-family` 里优先声明：
- `Noto Sans SC`（现代无衬线）、`Microsoft YaHei` / `SimHei`（黑体，通用）
- `Noto Serif SC` / `SimSun`（衬线 / 宋体，做古风、水墨风更好）
字体名含空格要加引号。

## 版式参考（同一份数据可快速出多版）
- **深色玄幻风**：深蓝黑渐变底 + 金/银/铜序号，标题金箔渐变文字。
- **浅色简约风**：米白底 + 白卡片 + 柔和阴影，序号用金/银/铜。
- **水墨古风**：宣纸底色 + 朱红印章 + 楷体序号（一~十）+ 细边框。
- **杂志卡片网格**：2 列卡片，每张卡大号 NO.x 徽章 + 书名 + 作者 + 一句话。

## 坑点（必看）
- **高度截断**：垂直 10 行榜单（1080 宽）真实高度约 2050–2160px，截图窗口设 `1080,2160` 才保险；2 列 10 卡网格真实高度约 1870px，窗口需 `≥1900`。原则是「CSS 里设 `min-height` 略大于预估，window-size 再取同一高度」。渲染后用 Read 打开 PNG 确认首尾都完整。
- **背景填充**：截图默认只截 window-size 区域。若页面 `min-height` 小于窗口高，多余区域会露出 body 背景色——用与海报一致的渐变铺满 `.poster` 即可无缝。
- **透明背景**：如需透明 PNG，加 `--default-background-color=00000000`，且不要给 body 设不透明背景。
- **中文引号 / 书名号**：HTML 里直接用中文《》"" 即可，截图渲染正常。
