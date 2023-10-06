# Hugo GitHub Pages 部署指南

歡迎使用 Hugo 快速建立個人網站！這個指南將引導你完成在 GitHub 上建立私人網站並部署到 GitHub Pages 的過程。

## 包含的內容

- `.gitignore`: 排除版本管理的檔案
- `.github/workflows/hugo.yml`: 使用 GitHub Action 將私人 Hugo 存放庫部署到公開的 GitHub Pages 存放庫。

## 步驟

1. 在 [GitHub](https://github.com/) 建立一個私人儲存庫 `hugo-site` 來管理你的網站原始碼，請記得包含 README.md 檔案。
2. 在 [GitHub](https://github.com/) 建立一個公開儲存庫 `{YOUR_USER_NAME}.github.io` 來上傳你的靜態網頁到 [GitHub Pages](https://pages.github.com/)。
3. 將 `hugo-site` 複製到本地：

   ```sh
   git clone https://github.com/{YOUR_USER_NAME}/hugo-site.git
   ```

   或者，如果你已經使用了 Git Submodule，可以使用以下方式複製：

   ```sh
   git clone --recursive https://github.com/{YOUR_USER_NAME}/hugo-site.git
   ```

4. 在 `hugo-site` 的同一層目錄創建 Hugo 專案（不要放在 `hugo-site` 裡面）：

   ```sh
   hugo new site hugo-site --force
   ```

5. 新增範例主題，這邊以 PaperMod 為例：

   ```sh
   cd hugo-site

   git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

   echo "theme = 'PaperMod'" >> hugo.toml
   ```

6. 將 [.gitignore](.gitignore) 檔案複製到 `hugo-site`。
7. [可選] 新增 GitHub Action 自動部署：

   ```sh
    mkdir -p .github/workflows/
    touch .github/workflows/hugo.yml
   ```

   將 [hugo.yml](.github/workflows/hugo.yml) 的內容複製到上述新增的空白 `hugo.yml`。請記得修改以下兩處：

   - **token: ${{ secrets.ACCESS_TOKEN }}**: 在這裡使用私人儲存庫的存取權杖（Access Token）。
   - **repository-name: YOUR_USER_NAME/YOUR_USER_NAME.github.io**: 將 `YOUR_USER_NAME` 改為你的 GitHub 帳號名稱。

8. 測試 Hugo 網站：

   ```sh
   hugo server -D
   ```

9. 開始創建自己的文章：

   ```sh
   hugo new posts/20231006/index.md
   ```

   在 `content/posts/20231006` 裡面的 `index.md` 開始撰寫，並將圖片放在同一個資料夾。

10. 恭喜你，已經完成私人儲存庫的設定，請不要忘記將變更提交到私人儲存庫。

## 參考資料

- [如何設定 ACCESS Token](https://github.com/JamesIves/github-pages-deploy-action/issues/624#issuecomment-791982883)
- [使用 GitHub Actions 將 Hugo 網站從私人儲存庫發佈到公開頁面](https://blog.euc-rt.me/post/github-actions-publish-private-hugo-repo-to-public-pages-site/)
- [Hugo 教學 -- 基礎篇](https://2ndbrain.cc/posts/2021/04/get-started-hugo/)
- [學習在幾分鐘內創建 Hugo 網站。](https://gohugo.io/getting-started/quick-start/)
