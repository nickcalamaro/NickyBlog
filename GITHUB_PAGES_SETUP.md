# GitHub Pages Setup Guide

This guide will help you deploy your Hugo site to GitHub Pages.

## Prerequisites

1. Your site code must be in a GitHub repository
2. You need admin access to the repository

## Setup Steps

### 1. Push Your Code to GitHub

If you haven't already, initialize a git repository and push your code:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

### 2. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click on **Settings** (top menu)
3. Click on **Pages** (left sidebar)
4. Under **Source**, select **GitHub Actions**

### 3. Configure Your Base URL (Important!)

Update your `hugo.toml` file to set the correct base URL:

- If using a custom domain: `baseURL = "https://yourdomain.com/"`
- If using GitHub Pages default: `baseURL = "https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/"`
- If your repo name matches your username: `baseURL = "https://YOUR_USERNAME.github.io/"`

**Example:**
```toml
baseURL = "https://username.github.io/hugoplate/"
```

### 4. Commit and Push

After updating `hugo.toml`:

```bash
git add hugo.toml
git commit -m "Update baseURL for GitHub Pages"
git push
```

### 5. Wait for Deployment

1. Go to the **Actions** tab in your GitHub repository
2. You should see the "Deploy Hugo site to Pages" workflow running
3. Wait for it to complete (usually 1-2 minutes)
4. Once complete, your site will be available at your GitHub Pages URL

## Troubleshooting

### Build Fails

- Check the Actions tab for error logs
- Ensure all dependencies are properly listed in `package.json`
- Make sure your Hugo version is compatible

### Site Doesn't Load Correctly

- Double-check your `baseURL` in `hugo.toml`
- Ensure it ends with a trailing slash `/`
- Clear your browser cache

### CSS/JS Not Loading

- This is usually a `baseURL` issue
- Make sure the `baseURL` matches your actual GitHub Pages URL exactly

## Workflow Details

The workflow (`.github/workflows/deploy.yml`) does the following:

1. Triggers on every push to the `main` branch
2. Installs Hugo Extended version
3. Installs Node.js and Yarn dependencies
4. Runs the theme generator script
5. Builds the Hugo site with minification
6. Deploys to GitHub Pages

## Manual Deployment

You can also trigger a deployment manually:

1. Go to **Actions** tab
2. Select "Deploy Hugo site to Pages"
3. Click **Run workflow**
4. Select the branch and click **Run workflow**

## Custom Domain (Optional)

To use a custom domain:

1. Add a file named `CNAME` to your `/static` folder with your domain
2. Configure your DNS settings with your domain provider
3. In GitHub Settings → Pages, enter your custom domain
4. Update `baseURL` in `hugo.toml` to your custom domain

---

For more information, visit: https://gohugo.io/hosting-and-deployment/hosting-on-github/
