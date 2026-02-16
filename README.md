# KSETA_2026
KSETA PhD course 2026 on EFT and experimental measurements 

## About This Course

This course provides an introduction to Effective Field Theory (EFT) and experimental measurements for PhD students. The course materials are provided as an interactive Jupyter Book.

## Viewing the Course

The course website will be automatically deployed to GitHub Pages at: [https://mpresill.github.io/KSETA_2026/](https://mpresill.github.io/KSETA_2026/)

### Enabling GitHub Pages

To enable GitHub Pages for the first time:

1. Go to your repository settings on GitHub
2. Navigate to "Pages" in the left sidebar
3. Under "Build and deployment", select "Source": **GitHub Actions**
4. The site will automatically build and deploy when you push to the `main` branch

After the first successful deployment, the website will be available at the URL above.

## Course Structure

The course website is organized into the following sections:

- **Course Overview**: Detailed course objectives and structure
- **Introduction to EFT**: Interactive Jupyter notebook with Python examples
- **Experimental Measurements**: Hands-on data analysis notebook
- **Slides**: Course presentation slides (add your slides to `slides.md`)
- **Tutorial**: Hands-on tutorial materials (add content to `tutorial.md`)
- **Supplementary Material**: Additional resources (add to `supplementary.md`)
- **References**: Bibliography and references (managed via `references.bib` and `references.md`)

## Building the Book Locally

To build and view the book locally on your machine:

1. Clone this repository:
   ```bash
   git clone https://github.com/mpresill/KSETA_2026.git
   cd KSETA_2026
   ```

2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Build the Jupyter Book:
   ```bash
   jupyter-book build .
   ```

4. Open the generated HTML in your browser:
   ```bash
   # On macOS
   open _build/html/index.html
   
   # On Linux
   xdg-open _build/html/index.html
   
   # On Windows
   start _build/html/index.html
   ```

## Editing the Course

To modify the course content:

1. **Edit content files**: Modify the markdown files (`.md`) or Jupyter notebooks (`.ipynb`)
2. **Update table of contents**: Edit `_toc.yml` to add or reorganize sections
3. **Modify configuration**: Update `_config.yml` for book settings
4. **Add references**: Add BibTeX entries to `references.bib`
5. **Push changes**: Commit and push to `main` - the website will automatically rebuild

## Adding Content

- **Slides**: Edit `slides.md` and add links to your slide files
- **Tutorial Materials**: Edit `tutorial.md` or add new Jupyter notebooks to the `notebooks/` directory
- **Supplementary Material**: Edit `supplementary.md`
- **References**: Add BibTeX entries to `references.bib` and organize them in `references.md`

## Configuration Files

- `_config.yml`: Main Jupyter Book configuration (title, author, repository links)
- `_toc.yml`: Table of contents structure
- `requirements.txt`: Python dependencies needed to build the book
- `.github/workflows/deploy.yml`: GitHub Actions workflow for automatic deployment

## Requirements

- Python 3.8+
- Jupyter Book 0.15.x
- NumPy, Matplotlib, SciPy (for running the example notebooks)

## Contributing

Contributions to improve the course materials are welcome! Please open an issue or submit a pull request.

## License

Course materials are provided for educational purposes.
