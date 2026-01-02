# LaTeX Document Template - User Manual

## Table of Contents

1. [Introduction](#introduction)
2. [Project Structure](#project-structure)
3. [Quick Start](#quick-start)
4. [Main Features](#main-features)
5. [Enhanced Code Blocks](#enhanced-code-blocks)
6. [Pseudocode Environments](#pseudocode-environments)
7. [Theorem Environments](#theorem-environments)
8. [Working with Images](#working-with-images)
9. [Customization](#customization)
10. [Tips and Tricks](#tips-and-tricks)
11. [Common Issues](#common-issues)
12. [Version Control](#version-control)
13. [Resources](#resources)

---

## Introduction

This is an academic LaTeX document template suitable for writing papers, reports, or literature reviews. It features modern code blocks with syntax highlighting and elegant pseudocode environments.

## Project Structure

```
.
├── main.tex                    # Main document entry file
├── main.pdf                    # Compiled PDF output
├── USAGE_EXAMPLES.tex          # Code and pseudocode examples
├── README.md                   # This complete user manual
├── compile.bat                 # Windows compilation script
├── .gitignore                  # Git ignore rules
├── config/                     # Configuration files
│   ├── _config.tex            # Global configuration (packages, fonts, environments)
│   ├── package.tex            # Package imports
│   ├── titlepage.tex          # Title page
│   ├── abstract.tex           # Abstract and keywords
│   ├── cover/                 # Cover page images
│   └── environments/          # Custom environments
│       ├── code.tex           # Code block environments
│       ├── theorem.tex        # Theorem environments
│       ├── custom.tex         # Custom text styles
│       └── figure.tex         # Figure environments
├── Chapters/                   # Chapter content
│   ├── chapter1/              # Chapter 1
│   │   ├── chap1.tex
│   │   └── images/            # Chapter 1 images
│   ├── chapter2/              # Chapter 2
│   │   ├── chap2.tex
│   │   └── images/            # Chapter 2 images
│   └── chapter3/              # Chapter 3
│       └── images/            # Chapter 3 images
├── Appendix/                   # Appendices
│   ├── Code/                  # Code appendix
│   │   └── code.tex
│   └── Supplementary/         # Supplementary materials
│       └── supplementary.tex
├── images/                     # Global images (shared across chapters)
└── References/                 # Bibliography
    └── Books/                 # Book references
        └── books.bib
```

## Quick Start

### 1. Compile the Document

Use the following commands to compile the main document:

```bash
# Full compilation (with bibliography)
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

Or use a LaTeX editor (e.g., TeXstudio, Overleaf) to compile `main.tex` directly.

### 2. View Examples

Compile `USAGE_EXAMPLES.tex` to see demonstrations of code blocks and pseudocode:

```bash
pdflatex USAGE_EXAMPLES.tex
```

### 3. Modify Document Information

Edit the following variables in `config/_config.tex`:

```latex
\def\myTitle{Your Document Title}
\def\myAuthor{Author Name}
\def\myDate{\today}  % or specify a date
\def\myAbstract{Your abstract content...}
\def\myKeywords{keyword1; keyword2; keyword3}
```

### 4. Add Chapter Content

Create new chapter folders and `.tex` files in the `Chapters/` directory, then include them in `main.tex`:

```latex
\input{Chapters/chapter3/chap3.tex}
```

### 5. Add References

Add bibliography entries in `References/Books/books.bib`, then cite them in your text using `\cite{citation_key}`.

### 6. Add Images

Place images in the appropriate directory:
- **Chapter-specific images**: `Chapters/chapter1/images/`, `Chapters/chapter2/images/`, etc.
- **Shared images**: `images/`
- **Cover images**: `config/cover/`

Insert images in your document:

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.8\textwidth]{myimage.png}
    \caption{Image caption}
    \label{fig:myimage}
\end{figure}
```

Reference the image in text:

```latex
As shown in Figure~\ref{fig:myimage}, the results demonstrate...
```

**See the "Working with Images" section below for detailed instructions.**

## Main Features

### Document Structure

- **Title Page**: Auto-generated cover with title, author, and date
- **Abstract**: Supports single or multi-paragraph abstracts with automatic formatting
- **Keywords**: Multiple keywords separated by semicolons
- **Table of Contents**: Automatically generated
- **Main Content**: Multi-chapter organization
- **Appendices**: Support for code, data, proofs, and other appendix types
- **Bibliography**: BibTeX-based reference management

### Page Numbering

- Abstract and TOC: Roman numerals (i, ii, iii...)
- Main content and appendices: Arabic numerals (1, 2, 3...)

## Enhanced Code Blocks

### Traditional Listings Environment

Use language-specific environments for basic code blocks:

```latex
\begin{pythoncode}
def hello_world():
    print("Hello, World!")
\end{pythoncode}
```

**Supported languages**: Python, JavaScript, Java, C++, C, MATLAB, R, SQL

### Modern Code Box (Recommended)

The `codebox` environment provides a modern, GitHub-style appearance:

```latex
\begin{codebox}{Python}
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
\end{codebox}
```

**Features**:
- Modern color scheme with syntax highlighting
- Line numbers with elegant styling
- Copy-friendly monospace font
- Automatic line breaking
- Rounded corners and subtle borders

### Code Box with Caption

Add a title/filename to your code block:

```latex
\begin{codeboxwithcaption}{JavaScript}{quicksort.js}
function quickSort(arr) {
    // Your code here
}
\end{codeboxwithcaption}
```

### Inline Code

Use inline code within text:

```latex
The \inlinecode{print()} function outputs text to the console.
```

### Supported Languages

- **Python**: Keywords, built-in functions, comments
- **JavaScript**: ES6+ syntax, async/await
- **Java**: Classes, interfaces, generics
- **C++**: Modern C++ features, STL
- **C**: Standard C syntax
- **MATLAB**: Functions, plotting commands
- **R**: Statistical functions, data frames
- **SQL**: Database queries, DDL/DML

## Pseudocode Environments

### Modern Pseudocode Box (Recommended)

The `pseudocode` environment creates elegant, numbered algorithm boxes:

```latex
\begin{pseudocode}{Binary Search}
\begin{algorithmic}[1]
\Require Array $A[1..n]$ sorted in ascending order, target value $x$
\Ensure Index of $x$ in $A$, or $-1$ if not found
\State $left \gets 1$
\State $right \gets n$
\While{$left \leq right$}
    \State $mid \gets \lfloor (left + right) / 2 \rfloor$
    \If{$A[mid] = x$}
        \State \Return $mid$
    \ElsIf{$A[mid] < x$}
        \State $left \gets mid + 1$
    \Else
        \State $right \gets mid - 1$
    \EndIf
\EndWhile
\State \Return $-1$
\end{algorithmic}
\end{pseudocode}
```

**Features**:
- Automatic numbering (Algorithm 1.1, 1.2, etc.)
- Purple color scheme for visual distinction
- Breakable across pages
- Professional typography
- Input/Output specifications with `\Require` and `\Ensure`

### Pseudocode Commands

- `\State`: Single statement
- `\If{condition}...\EndIf`: Conditional
- `\For{range}...\EndFor`: For loop
- `\While{condition}...\EndWhile`: While loop
- `\Function{name}{params}...\EndFunction`: Function definition
- `\Return`: Return statement
- `\Comment{text}`: Inline comment
- `\Require`: Input specification
- `\Ensure`: Output specification

### Traditional Algorithm Environment

For compatibility, the `breakablealgorithm` environment is also available:

```latex
\begin{breakablealgorithm}
\caption{Algorithm Name}
\begin{algorithmic}[1]
% Your algorithm here
\end{algorithmic}
\end{breakablealgorithm}
```

## Theorem Environments

### Standard Theorem Environments

```latex
\begin{theorem}
This is a theorem.
\end{theorem}

\begin{lemma}
This is a lemma.
\end{lemma}

\begin{definition}
This is a definition.
\end{definition}

\begin{proof}
This is a proof.
\end{proof}
```

**Available environments**: theorem, lemma, corollary, proposition, axiom, definition, example, remark, proof, solution

### Colored Box Environments

```latex
\begin{defn}[Optional Title]
This is a definition in a green box.
\end{defn}

\begin{Notice}[Custom Title]
This is an important notice.
\end{Notice}

\begin{examplebox}[Example Title]
This is an example in a cyan box.
\end{examplebox}
```

**Available boxes**: defn, axiombox, Notice, Proof, Derivation, examplebox

## Working with Images

### Image Directory Structure

The template has pre-configured image search paths. LaTeX will automatically find images in these directories:

```
images/                          # Global images (shared across all chapters)
config/cover/                    # Cover page images
Chapters/chapter1/images/        # Chapter 1 specific images
Chapters/chapter2/images/        # Chapter 2 specific images
Chapters/chapter3/images/        # Chapter 3 specific images
```

### Where to Put Your Images

#### Option 1: Chapter-Specific Images (Recommended)

Place images in the corresponding chapter's `images/` folder:

- **Chapter 1 images** → `Chapters/chapter1/images/`
- **Chapter 2 images** → `Chapters/chapter2/images/`
- **Chapter 3 images** → `Chapters/chapter3/images/`

**Advantages:**
- Better organization
- Easy to find images for specific chapters
- Can reuse same filename in different chapters

#### Option 2: Global Images

Place shared images in the root `images/` folder:

- **Logos, icons, common diagrams** → `images/`

**Advantages:**
- Accessible from any chapter
- Good for frequently used images
- Centralized location

#### Option 3: Cover Images

Place cover page images in:

- **Cover graphics** → `config/cover/`

### How to Insert Images

#### Basic Figure

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.8\textwidth]{myimage.png}
    \caption{This is my image caption}
    \label{fig:myimage}
\end{figure}
```

**Note:** No need to specify the full path, just the filename. LaTeX will search all configured directories.

#### Figure with Specific Width

```latex
\begin{figure}[H]
    \centering
    \includegraphics[width=10cm]{diagram.pdf}
    \caption{System architecture diagram}
    \label{fig:architecture}
\end{figure}
```

#### Figure with Scale

```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[scale=0.5]{photo.jpg}
    \caption{Scaled to 50\%}
    \label{fig:photo}
\end{figure}
```

#### Multiple Subfigures

```latex
\begin{figure}[htbp]
    \centering
    \begin{subfigure}{0.45\textwidth}
        \centering
        \includegraphics[width=\textwidth]{image1.png}
        \caption{First subfigure}
        \label{fig:sub1}
    \end{subfigure}
    \hfill
    \begin{subfigure}{0.45\textwidth}
        \centering
        \includegraphics[width=\textwidth]{image2.png}
        \caption{Second subfigure}
        \label{fig:sub2}
    \end{subfigure}
    \caption{Two subfigures side by side}
    \label{fig:combined}
\end{figure}
```

### Referencing Figures

After defining a label with `\label{fig:myimage}`, reference it in text:

```latex
As shown in Figure~\ref{fig:myimage}, the results demonstrate...
```

### Position Specifiers

| Specifier | Meaning |
|-----------|---------|
| `h` | Here (approximately) |
| `t` | Top of page |
| `b` | Bottom of page |
| `p` | On a separate page |
| `H` | Exactly here (requires `float` package) |
| `!` | Override internal parameters |

**Common combinations:**
- `[htbp]` - Try here, then top, then bottom, then separate page (recommended)
- `[H]` - Force exactly here (use sparingly)
- `[!htbp]` - More aggressive placement

### Size Options

#### Width-based

```latex
\includegraphics[width=0.8\textwidth]{image.png}    % 80% of text width
\includegraphics[width=10cm]{image.png}             % Exactly 10cm
\includegraphics[width=\linewidth]{image.png}       % Full line width
```

#### Height-based

```latex
\includegraphics[height=5cm]{image.png}             % Exactly 5cm tall
\includegraphics[height=0.3\textheight]{image.png}  % 30% of page height
```

#### Scale-based

```latex
\includegraphics[scale=0.5]{image.png}              % 50% of original size
\includegraphics[scale=1.5]{image.png}              % 150% of original size
```

### Supported Image Formats

#### Recommended Formats

- **PDF** - Best for vector graphics (diagrams, plots, flowcharts)
- **PNG** - Best for screenshots, raster images with transparency
- **JPG/JPEG** - Best for photos

#### Also Supported

- **EPS** - Encapsulated PostScript (older format)

### Best Practices for Images

#### 1. File Naming

✅ **Good:**
- `system_architecture.pdf`
- `experiment_results.png`
- `fig_chapter1_overview.jpg`

❌ **Avoid:**
- `图片1.png` (non-English characters)
- `my image.png` (spaces)
- `IMG_20240101.jpg` (unclear names)

#### 2. Organization Example

```
Chapters/chapter1/images/
├── fig1_introduction.png
├── fig2_methodology.pdf
└── fig3_results.png

Chapters/chapter2/images/
├── diagram_architecture.pdf
├── screenshot_interface.png
└── plot_performance.pdf

images/
├── logo.png
├── university_seal.pdf
└── common_icon.png
```

#### 3. Resolution Guidelines

- **Raster images (PNG/JPG):** 300 DPI for print, 150 DPI for screen
- **Vector images (PDF):** No resolution concerns
- **Screenshots:** Use original resolution, scale in LaTeX

#### 4. File Size

- Compress large images before including
- Use appropriate format (PDF for diagrams, JPG for photos)
- Keep total document size reasonable

### Advanced Image Options

#### Rotate Image

```latex
\includegraphics[angle=90, width=0.8\textwidth]{image.png}
```

#### Clip Image

```latex
\includegraphics[trim=1cm 2cm 1cm 2cm, clip, width=\textwidth]{image.png}
% trim=left bottom right top
```

#### Add Border

```latex
\fbox{\includegraphics[width=0.7\textwidth]{image.png}}
```

### Complete Image Example

```latex
\section{Results}

Figure~\ref{fig:performance} shows the performance comparison.

\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.9\textwidth]{performance_chart.pdf}
    \caption{Performance comparison across different methods. 
             The proposed method (blue) outperforms baseline methods 
             (red and green) in all test cases.}
    \label{fig:performance}
\end{figure}

As demonstrated in Figure~\ref{fig:performance}, our approach 
achieves superior results...
```

**Image location:** `Chapters/chapter1/images/performance_chart.pdf`

### Common Image Issues

#### Issue 1: Image Not Found

**Error:** `File 'image.png' not found`

**Solutions:**
1. Check image is in one of the configured directories
2. Verify filename spelling (case-sensitive on Linux)
3. Check file extension is correct
4. Ensure no spaces in filename

#### Issue 2: Image Too Large

**Error:** Image overflows page margins

**Solution:**
```latex
\includegraphics[width=\textwidth]{image.png}  % Fit to text width
```

#### Issue 3: Image in Wrong Position

**Problem:** Image appears far from where you want it

**Solutions:**
1. Use `[H]` for exact placement (requires `\usepackage{float}`)
2. Use `\FloatBarrier` to prevent floating past a point
3. Adjust figure placement preferences

## Customization

### Add Packages

Add required packages in `config/package.tex`.

### Custom Environments

Create custom environment files in `config/environments/`.

### Modify Styles

Edit document styles, fonts, and spacing in `config/_config.tex`.

### Color Customization

Modify color schemes in `config/environments/code.tex`:

```latex
\definecolor{codebg}{RGB}{248,249,250}        % Background
\definecolor{keywordcolor}{RGB}{215,58,73}    % Keywords
\definecolor{commentcolor}{RGB}{106,153,85}   % Comments
\definecolor{stringcolor}{RGB}{3,102,214}     % Strings
```

## Tips and Tricks

### Escape to LaTeX in Code

Use `(*@...@*)` to include LaTeX commands within code blocks:

```latex
\begin{codebox}{Python}
# Time complexity: (*@$O(\log n)$@*)
def binary_search(arr, target):
    pass
\end{codebox}
```

### Conditional Compilation

Control which chapters to compile by commenting/uncommenting in `main.tex`:

```latex
\def\allfiles{}  % Compile all chapters
% Comment out above line to compile specific chapters only
```

### Cross-References

Reference algorithms, theorems, and code:

```latex
\begin{pseudocode}{My Algorithm}
\label{alg:myalgorithm}
% ...
\end{pseudocode}

As shown in Algorithm~\ref{alg:myalgorithm}...
```

## Common Issues

### 1. Chinese Text Display

Ensure you're using `xelatex` or `pdflatex` with the `ctex` package installed.

### 2. Bibliography Not Showing

Make sure to run the complete compilation sequence:
```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

### 3. Compilation Errors

- Check the `.log` file for detailed error messages
- Verify all file paths are correct
- Check LaTeX syntax for errors
- Ensure all required packages are installed

### 4. Code Block Formatting Issues

- Use `\lstset{}` to adjust global settings
- Add `breaklines=true` for automatic line breaking
- Adjust `xleftmargin` and `xrightmargin` for margins

## Generated Files (Can Be Ignored)

Compilation generates auxiliary files that can be ignored or deleted:

- `*.aux` - Auxiliary files
- `*.log` - Log files
- `*.out` - Hyperlink information
- `*.toc` - Table of contents
- `*.bbl` - Bibliography list
- `*.blg` - BibTeX log

## Version Control

If using Git, add to `.gitignore`:

```
*.aux
*.log
*.out
*.toc
*.bbl
*.blg
*.synctex.gz
*.fdb_latexmk
*.fls
```

## Resources

- LaTeX Official Documentation: https://www.latex-project.org/
- CTEX Package Documentation: https://ctan.org/pkg/ctex
- BibTeX Guide: http://www.bibtex.org/
- Listings Package: https://ctan.org/pkg/listings
- Algorithm2e Package: https://ctan.org/pkg/algorithm2e
- TColorBox Manual: https://ctan.org/pkg/tcolorbox

## License

This template is free to use and modify.

---

**Happy LaTeXing!** 🎓
