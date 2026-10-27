# image-compression

## 目前狀態（2026-08-29）

- 本次未變更壓縮工具功能；工作區目前只有應用程式 `index.html` 與說明文件。
- 靜態檢查已通過：`index.html` 包含 `#root` 掛載點，5 個內嵌指令碼可由 Node.js 成功解析。
- 尚未在實際瀏覽器中以圖片驗證上傳、壓縮、重新壓縮、放大檢視，以及逐檔／ZIP 下載；這些端對端行為仍待驗證，不能視為已完成。

## 一句話
「LocalShrink」——單一 `index.html` 的純前端圖片壓縮工具，支援 PNG/JPEG/WebP，全部壓縮運算都在瀏覽器本機完成，圖片不上傳、不經伺服器。

## 狀態
功能看起來完整（拖拉上傳、品質滑桿、長邊尺寸上限、輸出格式選擇「智慧選擇/PNG/JPEG/WebP」、批次逐檔下載或打包 ZIP 下載、壓縮前後比較預覽、中英文雙語切換），但**這次盤點沒有實機開啟測試**，功能是否完全正常未驗證。原本的 `README.md` 只有一行 `"# ImageCompression"`，沒有任何說明，屬於這次補寫。

## 技術棧
- 單一 HTML 檔（`index.html`，約 1069 行），但內容其實是**打包產物**：內嵌了完整的 React 19 minified bundle（看得出是 esbuild/vite 之類工具打包後直接貼進同一個檔案），不是手寫 vanilla JS。
- 沒有留存原始的建置腳本/專案原始碼（`package.json`、React 元件原始檔等都不在這個資料夾裡），只有打包後的最終產物。
- 無後端、無外部 API 依賴；`.git` 資料夾存在但遠端/歷史細節未進一步查證。
- 圖片處理走瀏覽器內建 `<canvas>`／`toBlob` 一類的 API（依 UI 文案「重新編碼會自然移除 EXIF、GPS 與相機資訊」推斷，未逐行確認實作細節）。

## 怎麼跑起來
直接用瀏覽器開啟 `index.html`（雙擊或拖進瀏覽器視窗）即可，不需要 `npm install`、不需要伺服器、不需要網路連線（沒有外部 CDN 依賴）。

## 關鍵檔案
- `index.html` — 整個工具都在這一個檔案裡：`<style>` 區塊定義版面與元件樣式，中段是雙語文案替換的小型 script，後段是內嵌的 React runtime 與應用邏輯（含拖放上傳、壓縮設定、佇列/比較 UI）。

## 相關共用文件
- 適用工作流程：[[workflows/single-file-web-tool.md]]
- 相關教訓：[[lessons/naming-and-documentation-debt.md]]

## 原始位置
原本位於 `Desktop\coding\2026 project\ImageCompression\`，於 2026-08-18 遷移到此知識庫。
