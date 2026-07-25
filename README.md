<div align="center">

**[中文](#nmixx-演唱會應援練習頁面) | [English](#nmixx-concert-cheer-practice-page)**

</div>

---

# NMIXX 演唱會應援練習頁面

一個嵌入 WordPress 粉絲網站 [twnswer.com](https://twnswer.com/)（MIXX CLUB）的互動式應援練習工具，讓歌迷在演唱會前快速複習每首歌的應援法。純 HTML + CSS + JavaScript 打造，不依賴任何外部函式庫或框架。

## Demo

- 線上實際使用版本：[twnswer.com](https://twnswer.com/)
- 本機預覽：直接用瀏覽器打開任一 `*-standalone.html` 檔案即可

## 功能

- 左側歌單、右側應援內容，點歌即時切換，不用跳頁
- 歌曲依演出段落分組（Opening、Stage 1、Encore…），並用「應援」「純享」「Encore」三種標籤標示性質
- 應援法內容支援整行標色、行內局部標色兩種呈現方式，方便分辨「這句要喊」跟「這句用聽的」
- 有官方應援法的歌曲可嵌入對應的 YouTube 影片並指定起始時間點；沒有的歌曲顯示提示文字
- RWD：手機版把歌單收合成可展開選單，桌面版維持雙欄並排
- 所有樣式加上 `mixx-` 前綴，避免跟 WordPress 主題樣式衝突

## 開發過程（v1 → v3）

這個小工具是實際依照使用需求，分三次迭代做出來的：

| 版本 | 日期 | 改了什麼 |
|---|---|---|
| v1 | 2026/05/17 | 第一版可用版本：雙欄版面、點歌切換、RWD 手機收合選單 |
| v2 | 2026/06/06 | 右欄內容捲動時，歌名與標籤區塊改成「固定在頂部」（sticky），不會被捲走，看歌詞時更容易對照 |
| v3（最新） | 2026/06/28 | 桌面版隱藏側欄已顯示過的重複歌名、應援詞加上藍色粗體標示、曲目資料更新為最新場次、新增歌曲、每首歌加上影片起始時間點 |

## 檔案說明

每個版本都有兩份檔案：

- `應援區XXX版.html`：**WordPress 版**。設計成直接貼進 WordPress「自訂 HTML」區塊使用，字元編碼（charset）與版面寬度（viewport）由 WordPress 主題的 `<head>` 提供，所以檔案本身沒有這兩個設定。
- `應援區XXX版-standalone.html`：**獨立瀏覽版**。額外包了 `<!DOCTYPE>`、`<meta charset="UTF-8">`、`<meta name="viewport">`，可以直接雙擊在瀏覽器打開，或部署到 GitHub Pages 展示，不會因為缺少這兩項設定而中文亂碼、手機版失效。

> 這是實際測試後才發現的坑：獨立打開 WordPress 版檔案時，中文會變亂碼，手機版的收合選單也不會生效——因為瀏覽器在沒有 viewport 設定時，預設會用桌面版寬度（980px）渲染頁面，RWD 斷點永遠不會被觸發。

## 技術重點

- 純 HTML/CSS/JS，不使用 iframe 以外的外部資源
- 資料與畫面分離：所有歌詞與應援法整理成 JavaScript 物件（`CHEER_DATA`），改內容不用動版面邏輯
- RWD 斷點 768px，桌面/手機用同一份 CSS 依 media query 切換版面
- 專門處理 WordPress 客製 HTML 區塊的整合限制（class 前綴避免樣式衝突、無 iframe）

## 關於歌詞內容

頁面中部分歌曲附有完整韓文歌詞與應援法，僅作為粉絲練習用途，非商業使用。

---

如果你也在學做互動式網頁小工具，歡迎參考這個專案的資料/畫面分離寫法。

<br>
<br>

---

# NMIXX Concert Cheer Practice Page

An interactive cheer-practice tool embedded in the WordPress fan site [twnswer.com](https://twnswer.com/) (MIXX CLUB), built so fans can quickly review the fan-chant ("cheer") for each song before a concert. Built with plain HTML + CSS + JavaScript — no external libraries or frameworks.

## Demo

- Live version in use: [twnswer.com](https://twnswer.com/)
- Local preview: open any `*-standalone.html` file directly in a browser

## Features

- Two-pane layout — song list on the left, cheer content on the right — switches instantly on click, no page reload
- Songs grouped by set segment (Opening, Stage 1, Encore, …), tagged as "Cheer", "Listen only", or "Encore"
- Cheer lines support both full-line and inline partial highlighting, so it's easy to tell "shout this" from "just listen"
- Songs with an official cheer can embed the matching YouTube video at a specific start timestamp; songs without one show a fallback message
- Responsive: song list collapses into an expandable menu on mobile, stays as a fixed two-column layout on desktop
- All styles prefixed with `mixx-` to avoid conflicts with the WordPress theme's own styles

## Development History (v1 → v3)

This tool was built iteratively across three rounds, driven by real usage needs:

| Version | Date | What changed |
|---|---|---|
| v1 | 2026/05/17 | First working version: two-column layout, click-to-switch songs, mobile collapsible menu |
| v2 | 2026/06/06 | Song title/tag block in the right panel became sticky while scrolling through cheer content, so it stays visible for reference |
| v3 (latest) | 2026/06/28 | Desktop hides the now-redundant song title in the panel, cheer words highlighted in bold blue, setlist updated to the latest tour stop, new song added, video start-timestamps added per song |

## File Structure

Each version ships as two files:

- `應援區XXX版.html` — **WordPress version.** Meant to be pasted directly into a WordPress "Custom HTML" block; character encoding and viewport are provided by the WordPress theme's own `<head>`, so this file intentionally omits them.
- `應援區XXX版-standalone.html` — **Standalone version.** Wraps the same content with `<!DOCTYPE>`, `<meta charset="UTF-8">`, and `<meta name="viewport">` so it can be opened directly in a browser or deployed to GitHub Pages without breaking.

> This was a real bug found through testing, not a guess: opening the WordPress-version file standalone garbles the Chinese text and disables the mobile layout entirely — without a viewport meta tag, browsers default to a ~980px desktop-width viewport, so the mobile media query never fires.

## Technical Notes

- Pure HTML/CSS/JS, no external resources besides YouTube iframes
- Data/view separation: all lyrics and cheer data live in a single JavaScript object (`CHEER_DATA`), so content updates never touch layout logic
- Responsive breakpoint at 768px; desktop and mobile share one stylesheet via media queries
- Built around real constraints of embedding in a WordPress custom-HTML block (prefixed classes to avoid style collisions, no iframes for layout)

## On the Lyrics

Some songs include full Korean lyrics and cheer annotations, for non-commercial fan-practice use only.

---

If you're also learning to build small interactive web tools, feel free to reference this project's data/view separation approach.
