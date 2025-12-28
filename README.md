# Beamer Presentation Template

Minimal LaTeX template for academic presentations using **Beamer + Metropolis**.
Designed for local use, easy reuse, and clean separation between content and style.

---

## ✅ Requirements

* macOS
* **MacTeX** installed
* **VS Code**
* **LaTeX Workshop** extension

No additional configuration is required.

---

## 📁 Project Structure

```
.
├── main.tex                 # Main entry point (rarely modified)
├── config/
│   ├── packages.tex         # LaTeX packages
│   ├── theme.tex            # Colors, layout, title page, footer
│   └── commands.tex         # Custom macros
├── clases/
│   ├── clase01.tex          # One file per lecture
│   └── clase02.tex
├── images/
│   └── logos/
│       └── cenia_logo.png
└── README.md
```

---

## ▶️ How to Use

### 1. Create or edit a class

Edit or add a file inside:

```
clases/claseXX.tex
```

Each class contains its own sections and slides.

---

### 2. Select which class to compile

In `main.tex`:

```latex
\input{clases/clase02}
```

---

### 3. Compile

Just save the file.

VS Code + LaTeX Workshop will:

* Compile automatically
* Open the PDF
* Sync source ↔ PDF

---

## 🎨 Customization

### Theme & Layout

Edit:

```
config/theme.tex
```

Includes:

* Colors
* Header style
* Section slides
* Footer
* Title page

---

### Logo

Replace:

```
images/logos/cenia_logo.png
```

No other changes required.

---

### Section Slides

Section slides are created automatically using:

```latex
\section{Title}
```

Their appearance is controlled in `theme.tex`.

---

## ✅ Recommended Workflow

1. Duplicate this folder for a new course
2. Edit `main.tex`
3. Add or modify files in `clases/`
4. Compile

No need to touch the theme again.

---

## ✨ Notes

* Designed for academic lectures
* Clean, minimal style
* Works fully offline
* Compatible with Overleaf if needed

---

## Author

Custom Beamer template for teaching and academic presentations
