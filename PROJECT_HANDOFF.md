# 星域獵人 GALAXY STRIKER 專案交接紀錄

單檔 `index.html` 的瀏覽器飛機射擊遊戲。線上版：https://ternence503.github.io/galaxy-striker/ （GitHub Pages，repo 公開；改私有會讓免費方案的 Pages 失效，README 的 QR code 也就失效）。

## 現況（2026-10-05）
最後 commit `0617cdb`，已 push、工作樹乾淨。2026-10-05 一次大修（commit b24b9a1、94b23e2、6e86a43、0617cdb）：
- **Boss 觸發**：改用 `nextBossScore` 門檻（原 `score%區間` 會重複觸發，且分數 1–199 就誤觸）；擊殺後設為 `score+1000+level*500`。
- **雷射**：光束存活 6 幀、只在第一幀結算傷害。**導彈**：命中即消失、傷害 2、小爆炸（原本每幀扣血會秒殺 Boss）。
- **難度循序漸進**（使用者要求「第一關不能太難」）：Boss 血量 `40+level*20`；護盾第 2 關起才有、持續 `min(150,30+level*30)` 幀；開火間隔 `max(55,110-level*15)` 幀、彈幕種類 `min(3,level)`；被打中沿機身輪廓閃白光。
- **手機觸控**：Pointer Events、觸控時飛機停在手指上方 `TOUCH_OFFSET_Y=60`px、`touch-action:none`、`fitGame()` 等比縮小；音效鈕 48×44（`SOUND_BTN` 繪製與點擊判定共用）；Boss 血條上移（`by=H-68`）避免被武器提示框蓋住。
- README：真截圖 `screenshot.jpg`、QR code `qrcode.png`（用 OpenCV 解碼確認指向線上網址）。

## 驗證狀態
- **已實測**：Boss 觸發與血量、雷射／導彈行為、第 1 關／第 2 關護盾差異、觸控座標（模擬視窗 375×700，誤差 ≤2px）、音效鈕點擊判定。
- **未驗證（推測）**：手指偏移 60px 的手感、iOS 上音效能否出聲（通常要先點一下解鎖）、**第 2、3 關以後的難度曲線**（機器人測試被道具干擾，數據不可信）。

## 下一步／待辦
- 真機測試觸控手感與 iOS 音效，有問題再調 `TOUCH_OFFSET_Y`。
- 想讓更多人玩才考慮：最高分排行、更多關卡、社群推廣；目前定位是「作品集／練手」，使用者選擇只做低成本的真截圖＋QR。

## 注意
- 外接硬碟是 exFAT，會冒 `._*` 影子檔；commit 時只 `git add` 指定檔案。
- 測試技巧與坑（機器人≠真人難度、`javascript_tool` 45 秒逾時後背景測試殘留、無頭 Chrome 截遊戲要走 CDP 真實時間）見 Claude memory `feedback-game-testing-bot-and-headless-pitfalls`。
