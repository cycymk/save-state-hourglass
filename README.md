# 🫙 魔法能量瓶 StarJar

讓孩子用「完成好習慣」換「3C 時間」，App 當公正的裁判，家長不再當警察。

- 完整計畫：[docs/PLAN.md](docs/PLAN.md)
- 版本紀錄：[CHANGELOG.md](CHANGELOG.md)

## 在 iPad / 手機上安裝測試
1. 用 Safari 打開 GitHub Pages 網址（`https://<你的帳號>.github.io/<repo 名稱>/`）
2. 點「分享」→「加入主畫面」
3. 從主畫面開啟，就像 App 一樣全螢幕執行

> 麥克風（樂器練習）只能在 HTTPS 網址使用，GitHub Pages 已是 HTTPS。
> 想快速試玩：家長區（預設密碼 0000）→ 開啟「測試模式」，1 分鐘會縮短成 1 秒。

## 在電腦上本機執行
```bash
python -m http.server 8790 --directory app
```
然後打開 http://localhost:8790

## 專案結構
```
app/            網頁版 App（PWA，單一 index.html）
docs/PLAN.md    開發計畫與內容規劃
.github/        自動部署到 GitHub Pages
```
