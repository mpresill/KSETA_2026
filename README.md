# KSETA_2026
KSETA PhD course 2026 on EFT and experimental measurements

## Jupyter Book Course Website

This repository contains a Jupyter Book setup for the KSETA 2026 course materials.

### Structure

The course website is organized into the following sections:

- **Slides**: Course presentation slides (add your slides to `slides.md`)
- **Tutorial**: Hands-on tutorial materials (add your tutorial content to `tutorial.md`)
- **Supplementary Material**: Additional resources (add to `supplementary.md`)
- **References**: Bibliography and references (managed via `references.bib` and `references.md`)

### Building the Book Locally

1. Install the requirements:
   ```bash
   pip install -r requirements.txt
   ```

2. Build the book:
   ```bash
   jupyter-book build .
   ```

3. View the built site:
   ```bash
   # Open _build/html/index.html in your browser
   ```

### Deployment to GitHub Pages

The book is automatically deployed to GitHub Pages when you push to the `main` branch.

To enable GitHub Pages:
1. Go to your repository settings
2. Navigate to "Pages" under "Code and automation"
3. Under "Build and deployment", select "GitHub Actions" as the source
4. The site will be available at: `https://mpresill.github.io/KSETA_2026/`

### Adding Content

- **Slides**: Edit `slides.md` and add links to your slide files
- **Tutorial Materials**: Edit `tutorial.md` or add Jupyter notebooks
- **Supplementary Material**: Edit `supplementary.md`
- **References**: Add BibTeX entries to `references.bib` and organize them in `references.md`

### Configuration

- `_config.yml`: Main Jupyter Book configuration
- `_toc.yml`: Table of contents structure
- `requirements.txt`: Python dependencies 
