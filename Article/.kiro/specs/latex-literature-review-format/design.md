# Design Document: LaTeX Literature Review Format Conversion

## Overview

This design document outlines the conversion of an existing LaTeX book template to a literature review format. The conversion involves replacing the elaborate TikZ-based book cover with a simple academic title page, adding abstract and keywords sections, changing the document class from `ctexbook` to `ctexart`, and reorganizing the front matter to follow standard academic paper conventions.

The design maintains modularity through separate configuration files and preserves existing functionality for main content, appendices, and references while adapting the document structure for English-language academic writing.

## Architecture

### Document Structure

The reformed document will follow this structure:

```
1. Title Page (new page)
2. Abstract (new page)
3. Keywords (continuation of abstract page)
4. Table of Contents (new page)
5. Main Content (chapters → sections)
6. Appendices
7. References
```

### File Organization

```
.
├── main.tex                    # Main document entry point
├── config/
│   ├── _config.tex            # Global configuration and metadata
│   ├── package.tex            # Package imports
│   ├── titlepage.tex          # Title page layout (NEW)
│   ├── abstract.tex           # Abstract and keywords (NEW)
│   └── environments/          # Custom environments (unchanged)
├── Chapters/                  # Content chapters (structure unchanged)
├── Appendix/                  # Appendices (unchanged)
└── References/                # Bibliography files (unchanged)
```

### Key Changes

1. **Document Class**: `ctexbook` → `ctexart`
2. **Cover System**: Remove `config/cover.tex` and related files
3. **New Components**: Add `titlepage.tex` and `abstract.tex`
4. **Sectioning**: `\chapter` → `\section` throughout content files
5. **Language**: Chinese labels → English labels

## Components and Interfaces

### 1. Main Document (main.tex)

**Purpose**: Entry point that orchestrates all document components

**Interface**:
- Inputs: Configuration files, content files
- Outputs: Compiled PDF document

**Key Changes**:
```latex
% OLD
\documentclass[12pt, a4paper, oneside, UTF8]{ctexbook}
\input{config/cover}

% NEW
\documentclass[12pt, a4paper, oneside]{article}
\usepackage[UTF8]{ctex}
\input{config/titlepage}
\input{config/abstract}
```

### 2. Configuration File (_config.tex)

**Purpose**: Centralized metadata and configuration

**Interface**:
- Defines: Document metadata macros
- Used by: titlepage.tex, abstract.tex, main.tex

**New Metadata Fields**:
```latex
\def\myTitle{Document Title}
\def\myAuthor{Author Name}
\def\myDate{\today}
\def\myAbstract{Abstract content...}
\def\myKeywords{keyword1; keyword2; keyword3}
```

**Removed Fields**:
- `\myDateCover`
- `\myDateForeword`
- `\myForeword`
- `\myForewordText`
- `\mySubheading`
- `\myIndex`

### 3. Title Page (titlepage.tex)

**Purpose**: Generate simple academic title page

**Interface**:
- Inputs: `\myTitle`, `\myAuthor`, `\myDate` from _config.tex
- Outputs: Formatted title page

**Design**:
```latex
\begin{titlepage}
    \centering
    \vspace*{2cm}
    
    {\Huge\bfseries \myTitle \par}
    \vspace{2cm}
    
    {\Large \myAuthor \par}
    \vspace{1cm}
    
    {\large \myDate \par}
    
    \vfill
\end{titlepage}
```

### 4. Abstract and Keywords (abstract.tex)

**Purpose**: Display abstract and keywords sections

**Interface**:
- Inputs: `\myAbstract`, `\myKeywords` from _config.tex
- Outputs: Formatted abstract page

**Design**:
```latex
\newpage
\begin{abstract}
    \myAbstract
\end{abstract}

\noindent\textbf{Keywords:} \myKeywords
```

### 5. Package Configuration (package.tex)

**Purpose**: Load required LaTeX packages

**Key Changes**:
- Remove TikZ-related packages if only used for cover
- Ensure compatibility with `article` class
- Keep packages needed for content (theorem environments, code listings, etc.)

### 6. Content Files (Chapters/*.tex)

**Purpose**: Main document content

**Interface Changes**:
- `\chapter{Title}` → `\section{Title}`
- `\section{Title}` → `\subsection{Title}`
- `\subsection{Title}` → `\subsubsection{Title}`

**Note**: Files will need manual or automated conversion of sectioning commands

## Data Models

### Document Metadata

```latex
% Core metadata structure
{
    title: String,
    author: String,
    date: String,
    abstract: String,
    keywords: [String]  % semicolon-separated in LaTeX
}
```

### Page Numbering Scheme

```
Title Page:     no page number
Abstract:       Roman numerals (i, ii, ...)
TOC:            Roman numerals (continued)
Main Content:   Arabic numerals (1, 2, 3, ...)
```

## Correctness Properties

*A property is a characteristic or behavior that should hold true across all valid executions of a system—essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.*

### Property 1: Document Class Compatibility

*For any* LaTeX document using the new format, compiling with `pdflatex` or `xelatex` should produce a valid PDF without class-related errors.

**Validates: Requirements 5.1, 5.2**

### Property 2: Title Page Completeness

*For any* document metadata configuration, the title page should display all three required elements (title, author, date) in the correct order and formatting.

**Validates: Requirements 2.1, 2.2, 2.3, 2.4**

### Property 3: Abstract Placement

*For any* document with abstract content defined, the abstract section should appear immediately after the title page and before the table of contents.

**Validates: Requirements 3.1, 6.2**

### Property 4: Keywords Display

*For any* list of keywords defined in configuration, the keywords should appear after the abstract with the "Keywords:" label.

**Validates: Requirements 4.1, 4.2, 4.3, 4.4**

### Property 5: Front Matter Ordering

*For any* compiled document, the front matter components should appear in the exact order: title page, abstract, keywords, table of contents.

**Validates: Requirements 6.1, 6.2**

### Property 6: Page Numbering Consistency

*For any* document, front matter pages should use Roman numerals starting from the abstract, and main content should use Arabic numerals starting from 1.

**Validates: Requirements 6.4, 6.5**

### Property 7: Sectioning Command Compatibility

*For any* content file using `\section` commands (converted from `\chapter`), the document should compile without undefined command errors and produce correct section numbering.

**Validates: Requirements 5.3, 7.1**

### Property 8: Existing Functionality Preservation

*For any* document feature (appendices, references, custom environments), the functionality should work identically before and after the format conversion.

**Validates: Requirements 7.2, 7.3, 7.4, 7.5**

### Property 9: Configuration Modularity

*For any* metadata change in `_config.tex`, the change should propagate to all relevant document sections without requiring modifications to other files.

**Validates: Requirements 8.3, 8.4**

### Property 10: English Label Usage

*For any* automatically generated label (Abstract, Keywords, Contents, References), the label should appear in English.

**Validates: Requirements 9.1, 9.4**

## Error Handling

### Compilation Errors

1. **Missing Metadata**: If required metadata fields are undefined, provide default values:
   - `\myTitle` → "Untitled Document"
   - `\myAuthor` → "Anonymous"
   - `\myDate` → `\today`
   - `\myAbstract` → "(Abstract not provided)"
   - `\myKeywords` → ""

2. **Document Class Issues**: Ensure all packages are compatible with `article` class. Remove or replace book-specific commands.

3. **Sectioning Depth**: `article` class supports sections, subsections, and subsubsections. Deeper nesting may require custom configuration.

### Migration Issues

1. **Chapter References**: Any `\ref` commands pointing to chapters will need updating to point to sections.

2. **Page Layout**: Book-specific layout commands (e.g., `\cleardoublepage`) should be replaced with `\clearpage` or `\newpage`.

3. **TikZ Dependencies**: If TikZ is used elsewhere in the document, keep the package; otherwise, remove it to reduce compilation time.

## Testing Strategy

### Unit Tests

Since this is a LaTeX document transformation, "unit tests" take the form of compilation tests with specific configurations:

1. **Minimal Document Test**: Create a minimal document with only required metadata and verify it compiles.

2. **Full Metadata Test**: Test with all metadata fields populated and verify correct display.

3. **Empty Abstract Test**: Test with empty abstract string and verify graceful handling.

4. **Long Abstract Test**: Test with multi-paragraph abstract and verify proper formatting and page breaks.

5. **Many Keywords Test**: Test with 10+ keywords and verify proper display.

6. **Section Conversion Test**: Test a sample chapter file converted to sections and verify correct numbering.

7. **Cross-Reference Test**: Test that `\ref` and `\cite` commands work correctly after conversion.

8. **Appendix Test**: Verify appendices still work with `article` class.

9. **Bibliography Test**: Verify bibliography compilation with `bibtex` or `biblatex`.

### Integration Tests

1. **Full Document Compilation**: Compile the complete document with all chapters, appendices, and references.

2. **PDF Structure Verification**: Verify the PDF has correct bookmarks, page numbers, and navigation.

3. **Visual Inspection**: Manually review the PDF for formatting issues, spacing problems, and layout consistency.

### Testing Approach

- **Compilation Success**: Each test should result in successful PDF generation without errors.
- **Visual Validation**: Compare output against expected academic paper format.
- **Regression Testing**: Ensure existing content (theorems, code blocks, figures) still renders correctly.

### Test Execution

Tests will be executed by:
1. Modifying configuration files according to test case
2. Running `xelatex main.tex` (or `pdflatex`)
3. Checking for compilation errors in log file
4. Verifying PDF output matches expectations

**Note**: Property-based testing is not applicable to LaTeX document generation as it involves visual output rather than programmatic behavior. Testing relies on compilation success and visual verification.

## Implementation Notes

### Migration Path

1. **Backup**: Create backup of original files before modification
2. **Configuration**: Update `_config.tex` with new metadata structure
3. **Title Page**: Create `titlepage.tex` with simple academic layout
4. **Abstract**: Create `abstract.tex` for abstract and keywords
5. **Main File**: Update `main.tex` to use new document class and components
6. **Content**: Convert `\chapter` to `\section` in all content files
7. **Testing**: Compile and verify each component incrementally
8. **Cleanup**: Remove unused cover files and configurations

### Compatibility Considerations

- **Chinese Support**: Keep `ctex` package for potential Chinese content in main text
- **Font Selection**: Ensure fonts work with `article` class
- **Page Geometry**: May need to adjust margins for article format
- **Bibliography Style**: Verify bibliography style is appropriate for literature review

### Customization Options

Users can customize:
- Title page layout (spacing, font sizes)
- Abstract formatting (indentation, spacing)
- Keywords separator (semicolon, comma, etc.)
- Section numbering depth
- Page geometry (margins, paper size)
