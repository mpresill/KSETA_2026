# Setup Instructions for GitHub Pages

This document provides step-by-step instructions to enable GitHub Pages for your KSETA 2026 Jupyter Book course.

## Prerequisites

- Repository must be on GitHub
- You need admin access to the repository

## Steps to Enable GitHub Pages

### 1. Enable GitHub Pages with GitHub Actions

1. Go to your repository on GitHub: https://github.com/mpresill/KSETA_2026
2. Click on **Settings** (top menu bar)
3. In the left sidebar, scroll down and click on **Pages**
4. Under **Build and deployment**:
   - **Source**: Select **GitHub Actions** from the dropdown
   - This is important! GitHub Actions will automatically build and deploy your Jupyter Book

### 2. Merge or Push to Main Branch

Once you merge this PR or push the changes to the `main` branch, the GitHub Actions workflow will:
1. Automatically install dependencies
2. Build the Jupyter Book
3. Deploy it to GitHub Pages

### 3. Check Deployment Status

1. Go to the **Actions** tab in your repository
2. You should see a workflow run called "Deploy Jupyter Book"
3. Wait for it to complete (usually takes 2-3 minutes)
4. Once successful, your site will be available at: https://mpresill.github.io/KSETA_2026/

### 4. Verify the Website

Open https://mpresill.github.io/KSETA_2026/ in your browser. You should see:
- Welcome page with course information
- Navigation menu with course sections
- Interactive Jupyter notebooks

## Updating the Course

After initial setup, any changes pushed to the `main` branch will automatically trigger a rebuild and deployment:

1. Edit content files (`.md`, `.ipynb`)
2. Commit and push to `main`
3. GitHub Actions will automatically rebuild and deploy

## Troubleshooting

### Build Fails

If the GitHub Actions workflow fails:
1. Go to the **Actions** tab
2. Click on the failed workflow run
3. Check the error logs
4. Common issues:
   - Missing dependencies in `requirements.txt`
   - Syntax errors in notebooks or markdown files
   - Invalid configuration in `_config.yml` or `_toc.yml`

### GitHub Pages Not Enabled

If you don't see the Pages option in Settings:
1. Make sure your repository is public (or you have GitHub Pro for private repos)
2. Check that you have admin access to the repository

### 404 Error When Accessing Site

If you get a 404 error:
1. Wait a few minutes - first deployment can take 5-10 minutes
2. Check that the Actions workflow completed successfully
3. Verify GitHub Pages is set to "GitHub Actions" source

## Manual Build (Optional)

You can also build the book locally before pushing:

```bash
# Install dependencies
pip install -r requirements.txt

# Build the book
jupyter-book build .

# View locally
open _build/html/index.html
```

## Support

For issues with:
- **Jupyter Book**: https://jupyterbook.org/
- **GitHub Pages**: https://docs.github.com/en/pages
- **GitHub Actions**: https://docs.github.com/en/actions

## Next Steps

After enabling GitHub Pages:
1. Add more course content (lectures, exercises)
2. Customize the book appearance in `_config.yml`
3. Add more notebooks to the `notebooks/` directory
4. Update `_toc.yml` to include new sections
5. Share the website URL with students!
