# Pubilsh Notes

Simply zip whole folder as a zip file and upload to [Chrome Web Store](https://chrome.google.com/webstore/devconsole/1493e0a9-a65c-4e31-aefb-d9f27e0d8026/nkeadnckjdandlphpaniomonofdhlanb/edit/package).

## 第一次要手動部署到[開發人員資訊主頁](https://chrome.google.com/webstore/devconsole/)

```sh
$filePath = "Extension_v0.1.0.zip"
7z a $filePath _locales content background assets options popup CHANGELOG.md manifest.json README.*
(Get-ChildItem -Path . -Filter $filePath -Recurse | Select-Object -ExpandProperty FullName) | Set-Clipboard
```

## GitHub Actions

* [Use the Chrome Web Store Publish API](https://developer.chrome.com/docs/webstore/using-api)
* [如何使用 Chrome Web Store Publish API 自動化發佈 Chrome Extension](https://blog.miniasp.com/post/2025/02/07/How-to-use-the-Chrome-Web-Store-Publish-API-to-automate-the-publishing-of-a-Chrome-Extension?full=1)

### 申請 Chrome Web Store API 存取權限步驟說明

1. 建立 Google Cloud Project

   * 前往 [Google Cloud Console](https://console.cloud.google.com/)
   * 建立新專案
   * 啟用 Chrome Web Store API

2. 設定 OAuth 同意畫面

   ```markdown
   1. 側邊選單選擇「OAuth 同意畫面」
   2. 選擇「外部」使用者類型
   3. 填寫必要資訊：
      - 應用程式名稱
      - 使用者支援電子郵件
      - 開發人員聯絡資訊
   ```

3. 取得 `CLIENT_ID` 和 `CLIENT_SECRET`

   ```markdown
   1. 側邊選單選擇「憑證」
   2. 點選「建立憑證」→「OAuth 用戶端 ID」
   3. 應用程式類型選擇「桌面應用程式」
   4. 記下 `CLIENT_ID` 和 `CLIENT_SECRET`
   ```

4. 取得 `REFRESH_TOKEN`

   請透過 [OAuth 2.0 Playground](https://developers.google.com/oauthplayground/) 取得 Refresh Token (刷新金鑰)

5. 設定 GitHub Secrets

   參考文章說明: [如何使用 Chrome Web Store Publish API 自動化發佈 Chrome Extension](https://blog.miniasp.com/post/2025/02/07/How-to-use-the-Chrome-Web-Store-Publish-API-to-automate-the-publishing-of-a-Chrome-Extension?full=1)

注意事項：

* OAuth 同意畫面需要等待 Google 審核
* `REFRESH_TOKEN` 具有長期有效性，請妥善保管
* 建議在本機測試 API 呼叫是否正常運作
