# 〈反正〉imprv 段落選拔頁（fanzheng-imprv-vote）

## 目的
〈反正〉imprv 94 段 AOD（BlendVision 展示間短網址）做成一頁小遊戲：聰聰、佳豪、趙陽逐段試聽，
喜歡的段落按自己的名字；聽完「交卷」產生一條帶票的連結傳回來，我們打開該連結即匯入，在「排行」看統計。
GitHub Pages 靜態頁，範本來自 `Hsiao-Tzu/aolitu-foh-aod`（含試聽聲明橫幅）。

## 範圍鐵則
- 純靜態：無後端、無金鑰、不打 BlendVision API。票只存在各人瀏覽器 localStorage（key `fz-vote-v1`）。
- 統計靠交卷連結 `#v=<名字>:<段號.段號…>`（段號 1 起算＝頁面編號）；打開即覆蓋那個人的票（以最新一次交卷為準）。
- 播放在頁內：按「▶ 聽」在該列展開 BlendVision 官方嵌入播放器 `https://showroom.one.blendvision.com/embed?token=<token>&autoplay=true`（一次只開一段，收起＝移除 iframe＝停播）。
  `ROWS` 每列＝[段名, 展示間短網址, 嵌入 token]；token 取自短網址轉址後的 `?token=`。**不能嵌展示間首頁 `/?token=`**（iframe 內報 6001）。
  若 BV 端重產分享連結，token 會變，要重跑轉址抓 token 更新 `ROWS`。
- 段落資料只在 index.html 的 `ROWS` 常數，來源＝Drive 試算表「反正 短網址」(ID 19jFP6CzryrqG42V0SIoM8tGOEn8VQOUr98augCifBAY)。
  **段落順序不可改**：交卷連結用段號，改順序會讓舊連結對錯段。要加段只能加在尾端。
- 遊戲手感：先聽才能投（未聽按名字＝搖晃＋低音＋提示）、按下即壓（pointerdown）、放開彈出＋音高（聰 C5／佳 E5／趙 G5，三人全票＝C 大三和弦＋金色）、
  每 10 段里程碑音、全聽完彩帶。音效為 WebAudio 合成，無音檔；可靜音；尊重 prefers-reduced-motion。
- 頁面 `noindex`，但 repo 與網址公開，知道網址就能開。

## 退場條件
選拔結束、結果記下後：關 GitHub Pages、repo 封存或刪除。BlendVision 端 AOD 另行處理。

## 產出歸屬
- 正式網址：https://hsiao-tzu.github.io/fanzheng-imprv-vote/

## 改字流程（2026-11-12 使用者定）
- 使用者在桌面版 VS Code（Live Preview 邊改邊看）改文案、`Cmd+S` 存檔，不自己 commit；說「上線」由 Claude 接手。
- Claude：`git diff` 比對 → 檢查符號／標籤沒被改壞（有問題先說，不直接推）→ commit 說明格式 `文案：<改了哪裡>，<舊字> → <新字>` → 直推 `main` → 確認 Pages 出現新字才回報。
- 不走分支／PR／review（使用者定：只有本人改文案時維持直推）；日後有他人共編再改走 PR。
