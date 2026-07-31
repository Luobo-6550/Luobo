# html-poster-generator 使用说明

> 把榜单 / 排名表 / Top-N 清单 / 书单歌单等数据，生成可分享的高清海报图片（PNG）。

---

## 一、这是什么

一个「数据 → 海报图」的工作流 skill。核心思路：

**用 HTML + CSS 把数据排版好，再用 Microsoft Edge 无头模式截图成 PNG。**

为什么不直接用 AI 文生图？因为榜单里大量是中文专名和台词（书名、作者、金句），AI 生图基本必乱码。HTML 截图能保证中文 100% 清晰、排版可控、还能二次修改。

---

## 二、适用场景

- 用户给了一张排名表 / 清单 / Top-N 列表，并说「出图 / 做个图 / 生成海报 / 来张图」。
- 需要中文清晰、风格统一、可批量产出多种版式。
- 典型：网文榜单、电影 Top10、游戏排行、书单、歌单、年度盘点。

---

## 三、快速开始（3 步）

1. **写 HTML**：把数据写进一个自包含 HTML（CSS 内联，不依赖外部资源），存到当前工作目录。
2. **截图成 PNG**：用 Edge 无头模式渲染（命令见下方）。
3. **校验 + 交付**：用 Read 工具打开 PNG，确认首尾完整、无乱码；再 `present_files` 交付，并保留同名 `.html` 源文件方便改数据复用。

---

## 四、截图命令（Windows）

Edge 路径：`C:/Program Files (x86)/Microsoft/Edge/Application/msedge.exe`

```bash
EDGE="/c/Program Files (x86)/Microsoft/Edge/Application/msedge.exe"
D="C:/Users/72689/WorkBuddy/<日期目录>"

"$EDGE" --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --force-device-scale-factor=1 --window-size=1080,2160 \
  --screenshot="$D/out.png" "file://$D/out.html"
```

参数说明：
- `--window-size=W,H`：H 必须等于 / 超过页面真实高度，否则**底部被截断**。
- `--force-device-scale-factor=1`：1:1 像素，输出尺寸 = window-size。
- 其它系统把 Edge 换成对应 Chromium 内核浏览器（Chrome / Chromium）即可，参数一致。

---

## 五、可用中文字体（C:\Windows\Fonts）

CSS `font-family` 里优先声明（含空格要加引号）：
- 现代无衬线：`"Noto Sans SC"`、`"Microsoft YaHei"`、`SimHei`
- 衬线 / 古风：`"Noto Serif SC"`、`SimSun`

---

## 六、四种版式参考

同一份数据可快速出多版：
- **深色玄幻风**：深蓝黑渐变底 + 金/银/铜序号，标题金箔渐变文字。
- **浅色简约风**：米白底 + 白卡片 + 柔和阴影，序号金/银/铜。
- **水墨古风**：宣纸底色 + 朱红印章 + 楷体序号（一~十）+ 细边框。
- **杂志卡片网格**：2 列卡片，每张大号 NO.x 徽章 + 书名 + 作者 + 一句话。

---

## 七、常见坑（必看）

| 坑 | 现象 | 解决 |
|---|---|---|
| 高度截断 | 底部几行 / 几张卡消失 | window-size 的 H ≥ 页面真实高度。垂直 10 行榜单（1080 宽）≈ 2160；双列 10 卡网格 ≈ 1900。 |
| 背景露白 | 页面比窗口矮，底部露底色 | 给 `.poster` 铺与海报一致的渐变，自然填满。 |
| 透明背景需求 | 想要透明 PNG | 加 `--default-background-color=00000000`，且 body 不设不透明背景。 |
| 中文乱码 | 字体未命中 | `font-family` 显式声明上面的中文字体。 |

---

## 八、示例数据占位（替换即可）

```html
<div class="row">
  <div class="rank"><div class="no">NO.</div><div class="num">1</div></div>
  <div class="info">
    <div class="book">《书名》</div>
    <div class="author">作者</div>
  </div>
  <div class="tag">一句话记住它</div>
</div>
```

把上面这段按行复制、改内容，就能拼出任意长度的榜单。完整模板见同包的 `SKILL.md`。
