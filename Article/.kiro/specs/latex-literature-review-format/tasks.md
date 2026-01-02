# Implementation Plan: LaTeX Literature Review Format Conversion

## Overview

This plan converts the existing LaTeX book template to a literature review format by replacing the elaborate cover with a simple title page, adding abstract/keywords sections, changing the document class, and reorganizing the front matter. Tasks are ordered to ensure incremental progress with working compilation at each checkpoint.

## Tasks

- [x] 1. Backup and prepare configuration files
  - Create backup of original config/cover.tex and config/_config.tex
  - Update config/_config.tex with new metadata structure (remove cover-related fields, add abstract and keywords fields)
  - Remove cover-related package imports from config/package.tex if TikZ is only used for cover
  - _Requirements: 8.3, 8.4, 8.5_

- [x] 2. Create title page component
  - [x] 2.1 Create config/titlepage.tex with simple academic title page layout
    - Implement centered title, author, and date display
    - Use appropriate font sizes and spacing
    - Ensure title page occupies a single page
    - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5_

- [x] 2.2 Test title page with various metadata configurations
  - Test with minimal metadata (title only)
  - Test with full metadata (title, author, date)
  - Test with long titles that may wrap
  - _Requirements: 2.1, 2.2, 2.3_

- [-] 3. Create abstract and keywords component
  - [x] 3.1 Create config/abstract.tex for abstract and keywords sections
    - Implement abstract environment usage
    - Add "Keywords:" label with keyword display
    - Ensure proper spacing and formatting
    - _Requirements: 3.1, 3.2, 3.3, 3.4, 4.1, 4.2, 4.3, 4.4_

- [x] 3.2 Test abstract component with various content
  - Test with short abstract (single paragraph)
  - Test with long abstract (multiple paragraphs)
  - Test with empty abstract
  - Test with many keywords (10+)
  - _Requirements: 3.3, 3.5, 4.4_

- [x] 4. Update main document structure
  - [x] 4.1 Modify main.tex to use article document class
    - Change \documentclass from ctexbook to article
    - Add \usepackage[UTF8]{ctex} for Chinese support
    - Update document class options as needed
    - _Requirements: 5.1, 5.2, 9.2, 9.5_

  - [x] 4.2 Replace cover with title page and abstract in main.tex
    - Remove \input{config/cover} line
    - Add \input{config/titlepage} after \begin{document}
    - Add \input{config/abstract} after title page
    - Maintain proper page numbering setup
    - _Requirements: 1.1, 1.2, 6.1, 6.2_

  - [x] 4.3 Update front matter organization
    - Ensure title page has no page number
    - Set Roman numerals for abstract and TOC
    - Set Arabic numerals starting from main content
    - Remove foreword/preface sections
    - _Requirements: 6.1, 6.2, 6.3, 6.4, 6.5_

- [x] 5. Checkpoint - Compile document with new front matter
  - Compile main.tex and verify no errors
  - Check that title page, abstract, keywords, and TOC appear in correct order
  - Verify page numbering is correct
  - Ask user if any issues arise

- [x] 6. Convert chapter files to section-based structure
  - [x] 6.1 Update Chapters/chapter1/chap1.tex
    - Replace \chapter commands with \section
    - Replace \section commands with \subsection
    - Replace \subsection commands with \subsubsection
    - Update any chapter-specific references
    - _Requirements: 5.3, 5.5, 7.1_

  - [x] 6.2 Update Chapters/chapter2/chap2.tex
    - Apply same sectioning command conversions as chapter1
    - _Requirements: 5.3, 5.5, 7.1_

  - [x] 6.3 Check for and update chapter3 if it exists
    - Apply sectioning command conversions
    - _Requirements: 5.3, 5.5, 7.1_

- [x] 6.4 Test sectioning and cross-references
  - Verify section numbering is correct
  - Test \ref commands pointing to sections
  - Verify TOC displays sections correctly
  - _Requirements: 5.5, 7.5_

- [x] 7. Update appendix structure for article class
  - [x] 7.1 Verify appendix files compile with article class
    - Check Appendix/Code/code.tex
    - Check Appendix/Supplementary/supplementary.tex
    - Update any book-specific commands (e.g., \cleardoublepage → \clearpage)
    - _Requirements: 7.2_

- [x] 7.2 Test appendix functionality
  - Verify appendices appear after main content
  - Verify appendix numbering (A, B, C...)
  - Test cross-references to appendix sections
  - _Requirements: 7.2, 7.5_

- [x] 8. Verify bibliography and references
  - [x] 8.1 Check bibliography compilation
    - Ensure bibliography style works with article class
    - Verify \bibliography command in main.tex
    - Update bibliography heading if needed (chapter → section)
    - _Requirements: 7.3_

- [x] 8.2 Test bibliography functionality
  - Compile with bibtex/biber
  - Verify citations appear correctly in text
  - Verify reference list appears correctly
  - _Requirements: 7.3, 7.5_

- [x] 9. Update English labels and language settings
  - [x] 9.1 Configure English labels in document
    - Ensure "Abstract" appears in English (not "摘要")
    - Ensure "Keywords" appears in English
    - Ensure "Contents" appears in English (not "目录")
    - Ensure "References" appears in English
    - Add language options to document class or packages as needed
    - _Requirements: 9.1, 9.2, 9.4_

- [x] 9.2 Test English label display
  - Compile document and verify all labels are in English
  - Verify Chinese content in main text still displays correctly
  - _Requirements: 9.1, 9.4, 9.5_

- [x] 10. Clean up unused files
  - [x] 10.1 Remove or archive cover-related files
    - Move config/cover.tex to backup or delete
    - Move config/cover/ directory to backup or delete
    - Remove cover-related variables from _config.tex if any remain
    - _Requirements: 1.1, 1.2, 1.3_

- [x] 11. Final checkpoint - Full document compilation and verification
  - Compile complete document with all chapters, appendices, and references
  - Verify PDF structure: title page → abstract → keywords → TOC → content → appendices → references
  - Check page numbering throughout document
  - Verify all cross-references work correctly
  - Verify all custom environments (theorems, code blocks) still work
  - Ask user to review final output

## Notes

- All tasks are required for comprehensive testing and validation
- Each task references specific requirements for traceability
- Checkpoints ensure incremental validation of the conversion
- The conversion maintains all existing functionality while adapting the document structure
- Manual review of the final PDF is essential to verify visual formatting
