# 魔法能量瓶（StarJar）— 給 Claude 的專案說明

給台灣國小 / 國中生的遊戲化時間管理工具：完成好習慣任務 → 累積「星露」→ 裝滿魔法瓶 → 換 3C 遊戲時間。
完整產品規劃見 `docs/PLAN.md`（防沉迷機制、防賴皮設計、版本排程都在裡面），請以它為準。

## 專案結構
- `app/index.html`：整個 App（HTML + CSS + JS 單檔，無建置步驟、無外部相依）
- `app/sw.js`：Service Worker，**每次發版都要把 `CACHE` 名稱改成新版本號**，否則 iPad 會拿到舊快取
- `app/manifest.webmanifest`、`app/icon-*.png`：PWA 安裝用
- `docs/PLAN.md`：開發計畫；`docs/FEEDBACK.md`：家長試玩回饋；`CHANGELOG.md`：版本紀錄
- `.github/workflows/pages.yml`：main → 正式站、dev → `/beta/` 試玩站

## 開發慣例
- 介面文字一律**繁體中文（台灣用語）**，語氣溫和、不用懲罰性字眼（用「魔法陣暫停了」而不是「你失敗了」）
- 兩套主題（`data-theme="kid"` / `"teen"`），新介面兩套都要好看；顏色只用 `:root` 上的 CSS 變數
- 觸控目標 ≥ 48px；要能在 iPad 直 / 橫向與手機寬度（375px）正常顯示
- 資料存在 `localStorage`（`db` 物件），**修改資料結構時必須相容舊資料**（用預設值補欄位，絕不能清掉孩子的紀錄）
- 紀錄（`db.logs`）不可刪除，這是產品承諾
- 不使用任何有版權的角色或素材；吉祥物是原創的「露米」
- 不加入廣告、追蹤或把資料送到外部伺服器
- 註解用繁體中文，簡短即可，風格跟現有程式一致

## 本機測試
```bash
python -m http.server 8790 --directory app
```
家長區預設密碼 `0000`；家長區可開「測試模式」（1 分鐘 = 1 秒）。

## 每週發版流程（雲端排程使用）
1. 從 `main` 更新 `dev`（`git checkout dev && git merge origin/main`），在 `dev` 上開發
2. 先處理 `docs/FEEDBACK.md`「待處理」，再依 `docs/PLAN.md` 第 12 節排程做下一版
3. 一週只做一個版本、範圍要小而完整，寧可少做也不要做壞
4. 自我檢查：JS 語法（`node --check` 抽出的 script）、舊資料相容、兩套主題、手機寬度
5. 更新 `app/sw.js` 的 `CACHE`、`CHANGELOG.md`、`docs/FEEDBACK.md`
6. 推送 `dev`，並開 / 更新 `dev → main` 的 PR，PR 說明寫給家長看（改了什麼、怎麼試、需要家長決定的事）
7. 家長在 `/beta/` 試玩後合併 PR，正式站才會更新
