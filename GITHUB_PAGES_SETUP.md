# GitHub Pages Setup Instructions

## Quick Setup Steps

### 1. Commit and Push Your Changes
First, commit the updated files and push to GitHub:

```bash
git add docs/index.md docs/_config.yml
git commit -m "Configure GitHub Pages with Jekyll"
git push origin main
```

*(Replace `main` with your branch name if different - could be `master`)*

### 2. Configure GitHub Pages Settings

1. Go to your repository on GitHub: `https://github.com/YOUR_USERNAME/nautical_systems`
2. Click on **Settings** tab
3. In the left sidebar, click on **Pages** (under "Code and automation")
4. Under **Build and deployment**:
   - **Source**: Select "Deploy from a branch"
   - **Branch**: Select your main branch (e.g., `main` or `master`)
   - **Folder**: Select `/docs` 
5. Click **Save**

### 3. Wait for Deployment

- GitHub will automatically build and deploy your site
- This usually takes 1-2 minutes
- You'll see a message at the top with your site URL: `https://YOUR_USERNAME.github.io/nautical_systems/`

### 4. Check Deployment Status

- Go to the **Actions** tab in your repository
- You should see a "pages build and deployment" workflow running
- Once it completes (green checkmark), your site is live!

## Your Site Structure

Your GitHub Pages site will be published from the `/docs` folder:

- **Homepage**: `docs/index.md` → `https://YOUR_USERNAME.github.io/nautical_systems/`
- **Other docs**: Available through relative links on the homepage

## Troubleshooting

### Issue: Site not updating
- Check the Actions tab for build errors
- Make sure you pushed to the correct branch
- Wait a few minutes and hard refresh (Ctrl+F5)

### Issue: Images not showing
- Check that image paths are correct (relative to the docs folder)
- Images should use `../media/` paths since they're outside the docs folder
- Spaces in filenames should be URL-encoded: `%20`

### Issue: Links not working
- Use relative links (e.g., `../NS_Release_Notes_7.md`)
- Avoid Obsidian wiki-link syntax (`[[...]]`)
- Standard markdown links: `[Link Text](path/to/file.md)`

## Customization

### Change Theme
Edit `docs/_config.yml` and change the theme line:
```yaml
theme: jekyll-theme-slate
# Other options: cayman, minimal, modernist, tactile, etc.
```

### Add More Pages
Just add more `.md` files in the `docs/` folder and link to them from `index.md`

## Next Steps

1. Consider moving all documentation files into the `docs/` folder for better organization
2. Update internal links between documents
3. Add a custom domain if desired (Settings → Pages → Custom domain)
4. Make the repository public if it's currently private (required for GitHub Pages on free plan)

---

**Note**: GitHub Pages sites are publicly accessible even if your repository is private (with GitHub Pro or higher).

