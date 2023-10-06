# Hugo Github Pages Deployment Guide

Welcome to the world of Hugo, where you can swiftly create your personal website! This guide will walk you through the process of creating a private website on GitHub and deploying it to GitHub Pages.

## Included Contents

- `.gitignore`: Excludes files from version control.
- `.github/workflows/hugo.yml`: Uses GitHub Actions to deploy your private Hugo repository to a public GitHub Pages repository.

## Steps

1. Create a private repository `hugo-site` on [GitHub](https://github.com/) to manage your website source code, ensuring to include the README.md file.
2. Create a public repository `{YOUR_USER_NAME}.github.io` on [GitHub](https://github.com/) to upload your static web pages to [GitHub Pages](https://pages.github.com/).
3. Clone `hugo-site` to your local machine:

   ```sh
   git clone https://github.com/{YOUR_USER_NAME}/hugo-site.git
   ```

   Alternatively, if you are using Git Submodules:

   ```sh
   git clone --recursive https://github.com/{YOUR_USER_NAME}/hugo-site.git
   ```

4. Create a Hugo project in the same directory as `hugo-site` (not inside `hugo-site`):

   ```sh
   hugo new site hugo-site --force
   ```

5. Add an example theme. Here, we'll use PaperMod as an example:

   ```sh
   cd hugo-site

   git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

   echo "theme = 'PaperMod'" >> hugo.toml
   ```

6. Copy the [.gitignore](.gitignore) file into `hugo-site`.
7. [Optional] Set up GitHub Action for automatic deployment:

   ```sh
    mkdir -p .github/workflows/
    touch .github/workflows/hugo.yml
   ```

   Copy the contents of [hugo.yml](.github/workflows/hugo.yml) into the newly created `hugo.yml` file. Remember to modify these two parts:

   - **token: ${{ secrets.ACCESS_TOKEN }}**: Use a personal access token for this private repository.
   - **repository-name: YOUR_USER_NAME}}/YOUR_USER_NAME.github.io**: Replace `YOUR_USER_NAME` with your GitHub username.

8. Test your Hugo website:

   ```sh
   hugo server -D
   ```

9. Start writing your own posts:

   ```sh
   hugo new posts/20231006/index.md
   ```

   Begin writing in `index.md` inside `content/posts/20231006`, and place images in the same folder.

10. Congratulations, you've configured your private repository! Don't forget to commit your changes to the private repository. Best of luck creating your beautiful website!

## References

- [How to setup ACCESS Token](https://github.com/JamesIves/github-pages-deploy-action/issues/624#issuecomment-791982883)
- [Using GitHub Actions to Publish Hugo Site From Private to Public Repo](https://blog.euc-rt.me/post/github-actions-publish-private-hugo-repo-to-public-pages-site/)
- [Learn to create a Hugo site in minutes.](https://gohugo.io/getting-started/quick-start/)
