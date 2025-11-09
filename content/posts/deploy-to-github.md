+++
date = '2025-11-08T21:46:01-05:00'
draft = false
title = 'Deploy to Github'
+++

I've set up automatic deployment of your Hugo site to GitHub Pages. Here's what was done:

- Updated the `baseURL` in `hugo.toml` to `https://yoloinfinity55.github.io/hugo-mac/`
- Created a GitHub Actions workflow (`.github/workflows/deploy.yml`) that builds the site and deploys it to the `gh-pages` branch on every push to `main`
- Committed and pushed the changes to trigger the first deployment

The workflow will automatically build your Hugo site using the latest Hugo version and deploy the generated static files to GitHub Pages.

__Next steps (you need to do this manually):__

1. Go to your repository on GitHub ([](https://github.com/yoloinfinity55/hugo-mac)<https://github.com/yoloinfinity55/hugo-mac>)
2. Navigate to Settings > Pages
3. Under "Source", select "Deploy from a branch"
4. Choose the `gh-pages` branch and `/ (root)` folder
5. Save the settings

Once enabled, your site will be live at [](https://yoloinfinity55.github.io/hugo-mac/.)<https://yoloinfinity55.github.io/hugo-mac/.> The first deployment may take a few minutes after the workflow completes.
