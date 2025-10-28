# GitHub Pages Setup - Quick Start

## Step 1: Commit and Push

```bash
git add docs/
git commit -m "Setup GitHub Pages documentation"
git push origin master
```

## Step 2: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under **Build and deployment**:
   - **Source**: Deploy from a branch
   - **Branch**: `master`
   - **Folder**: `/docs`
4. Click **Save**

## Step 3: Access Your Site

Wait 1-2 minutes, then visit:
```
https://YOUR_USERNAME.github.io/nautical_systems/
```

That's it! Every time you push changes to the docs folder, GitHub will automatically rebuild your site.

---

## What's Published

Everything in the `/docs` folder:
- `index.md` - Homepage
- All documentation `.md` files
- All images in `media/` folder

## Troubleshooting

**Site not updating?**
- Check **Actions** tab for build errors
- Wait a few minutes and hard refresh (Ctrl+F5)

**Images not showing?**
- Make sure image paths use `media/` (relative path)
- Check that media folder is in docs/

**Need a different theme?**
Edit `docs/_config.yml`:
```yaml
theme: jekyll-theme-slate
# Options: cayman, slate, minimal, modernist, tactile
```

