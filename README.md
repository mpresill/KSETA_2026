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

## Course Structure

The course includes:
- **Introduction**: Course overview and objectives
- **EFT Theory**: Theoretical foundations of Effective Field Theory
- **Experimental Methods**: Detector principles and data analysis
- **Interactive Notebooks**: Hands-on exercises using Jupyter notebooks

## Editing the Course

To modify the course content:

1. Edit the markdown files (`.md`) or Jupyter notebooks (`.ipynb`) in the repository
2. Update the table of contents in `_toc.yml` if adding new sections
3. Modify the book configuration in `_config.yml` as needed
4. Push changes to the `main` branch - the website will automatically rebuild and deploy

## Requirements

- Python 3.8+
- Jupyter Book
- NumPy, Matplotlib, SciPy (for running the example notebooks)

## Contributing

Contributions to improve the course materials are welcome! Please open an issue or submit a pull request.

## License

Course materials are provided for educational purposes.
