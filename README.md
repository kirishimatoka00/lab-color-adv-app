# Lab Gamut Simulator（Lab 色域模擬器）

在 Lab 色彩空間中輸入 Base / History / Test 點，即時以 3D 與 2D 檢視色域範圍、ΔE 與色域修正量。支援 Excel 匯入／匯出、相機取色，並可打包成 Android APK 安裝在手機上。

## 在手機上安裝 APK

1. 到本 repo 的 **Releases** 頁面，下載最新的 `lab-color-adv-app.apk`（標籤為 `latest`）。
2. 用手機開啟下載的 APK，依提示允許「安裝未知來源應用程式」後安裝。
3. 之後有新版本時直接下載新的 APK 覆蓋安裝即可（簽章固定，資料不會消失）。

APK 由 GitHub Actions 自動建置：每次推送到 `main`，或在 **Actions → Build Android APK → Run workflow** 手動執行，都會產生新的 APK。建置約需 5～10 分鐘。

> 這個 APK 使用 repo 內公開的固定 keystore（`android/keystore/debug.keystore`）簽署，僅供個人／內部自用，不適合上架 Google Play。

## 手機版面

- 手機（寬度小於 768px）：底部分頁切換 **Points（資料）** 與 **Viewer（視圖）**；視圖右上角的全螢幕按鈕可放大單一視圖。
- 平板與桌機：維持左右並排。
- 匯出 Excel／儲存截圖：在 APK 內會開啟系統分享面板，可儲存到檔案、雲端硬碟或傳給其他 App。

## 本機開發

需要 Node.js 22 以上。

```bash
npm install
npm run dev        # 開發伺服器
npm run build      # 打包網頁到 dist/
```

## 本機建置 APK（選用）

需要 JDK 21 與 Android SDK（或直接用 Android Studio）。

```bash
npm run android:sync          # 打包網頁並同步到 android/
cd android && ./gradlew assembleDebug
# 輸出：android/app/build/outputs/apk/debug/app-debug.apk
```

## 專案結構

| 路徑 | 說明 |
| --- | --- |
| `src/main.jsx` | 應用程式主體（React + react-three-fiber） |
| `src/index.css` | Tailwind 與全域樣式 |
| `capacitor.config.json` | Capacitor 設定（App 名稱、ID、狀態列） |
| `android/` | Capacitor 產生的 Android 專案（相機權限、簽章、圖示已設定） |
| `.github/workflows/build-apk.yml` | 自動建置 APK 並發佈到 Releases |
