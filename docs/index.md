# Publishing Documentation with GitHub Pages

Welcome! This site demonstrates how to publish documentation to the web using **GitHub Pages** - a free static site hosting service from GitHub.

## What is GitHub Pages?

GitHub Pages allows you to turn your GitHub repository into a live website. It's perfect for:

- **Project documentation** - Share guides, manuals, and technical docs
- **Knowledge bases** - Create searchable repositories of information  
- **Personal websites** - Blogs, portfolios, and project showcases
- **Team collaboration** - Publish internal documentation for your organization

## How It Works

GitHub Pages uses **Jekyll**, a static site generator, to convert your Markdown files into a website:

1. Write content in **Markdown** (`.md` files)
2. Push to your **GitHub repository**
3. Configure **GitHub Pages** in repository settings
4. Your site is **automatically published** to the web!

## Publishing Options

### Option 1: Deploy from a Branch (Recommended for Simple Sites)

This is the easiest method - perfect for documentation sites like this one:

- Select a **branch** (e.g., `main` or `master`)
- Choose a **folder** (`/` root or `/docs`)
- Push changes to automatically rebuild your site
- No custom build process needed

**Best for:** Documentation, guides, and simple static sites

### Option 2: GitHub Actions Workflow (Advanced)

Use a custom workflow for more control over the build process:

- Write a **custom GitHub Actions workflow**
- Use any static site generator (Hugo, Gatsby, Next.js, etc.)
- Add build steps, tests, and custom deployment logic
- Trigger builds manually or on pull requests

**Best for:** Complex sites, custom build tools, or non-Jekyll generators

## Key Features

✅ **Free hosting** for public repositories  
✅ **Custom domains** supported (e.g., docs.yourcompany.com)  
✅ **HTTPS enabled** automatically for security  
✅ **Version control** - track all changes with Git  
✅ **Easy updates** - just push to deploy  
✅ **Multiple themes** available out of the box  

## This Site's Setup

This documentation site uses:

- **Publishing source:** `/docs` folder on the main branch
- **Theme:** Jekyll Cayman theme
- **Content format:** Markdown files with images
- **Deployment:** Automatic on every push

## Example Documentation

Here are some sample documents published on this site:

- [Release Notes 7.0](../NS_Release_Notes_7.md)
- [VM-Mooring User Guide 6.5.36](../NS_VM-Mooring_User_Guide%206.5.36.md)
- [Work Order Import Reference Guide 7.0.0](../NS_Work_Order_Import_Reference_Guide_7.0.0.md)
- [Azure Cloud Installation Guide 7.0.0](../NS_Azure_Cloud_Installation_Guide_7.0.0.md)

## Getting Started

To create your own GitHub Pages site:

1. **Create a repository** on GitHub
2. **Add Markdown files** (like `index.md`)
3. **Go to Settings → Pages** in your repository
4. **Select your publishing source** (branch and folder)
5. **Save** and wait a few minutes for deployment

Your site will be available at: `https://YOUR_USERNAME.github.io/REPOSITORY_NAME/`

## Resources

- 📖 [GitHub Pages Documentation](https://docs.github.com/en/pages)
- 🎨 [Jekyll Themes](https://pages.github.com/themes/)
- ✍️ [Markdown Guide](https://www.markdownguide.org/)
- ⚙️ [Jekyll Documentation](https://jekyllrb.com/docs/)

---

**Ready to publish your own documentation?** Check out the [GitHub Pages setup guide](../GITHUB_PAGES_SETUP.md) in this repository!