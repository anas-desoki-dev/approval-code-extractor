# Universal Document Nomenclature & Approval Extractor

Desktop tool for Document Controllers that extracts consultant approval codes (A/B/C/D) from digital PDF submittals by analyzing the vector markup and text coordinates, and standardizes folder and archive names to a fixed naming convention.

## ⚠️ Repository Note
*This repository serves as a portfolio showcase of the architectural logic, spatial PDF parsing techniques, and UI/UX design. The proprietary Python source code is withheld to protect intellectual property.*

## 🚧 The Problem
In the construction industry, all types of submittals are returned by consultants with digital markups indicating the approval status (Code A, B, C, or D). 
1. **Manual Data Entry:** Document Controllers must open hundreds of diverse PDFs daily just to check the stamp and log the code into an Excel tracker.
2. **Naming Inconsistencies:** Files and ZIP archives are often named chaotically by different engineers, breaking the project's strict nomenclature and causing sorting collisions.

## 💡 The Solution & Core Features

### 1. Universal Approval Extraction (Native Digital PDFs)
* **Vector Geometry Detection:** Rather than relying on heavy OCR, the engine utilizes `PyMuPDF` to instantly scan digital (native) PDFs for specific vector shapes (e.g., bounding boxes or rectangles) drawn by consultants, **regardless of the markup color used**.
* **Coordinate-Based Text Extraction:** Once a markup boundary is detected, the engine calculates the coordinates and extracts the text (A, B, C, or D) located within or immediately adjacent to the bounding box.
* **Submittal Agnostic:** Works on any native digital PDF, regardless of submittal type (QC, IR, MIR, RFIs) as long as it is a native digital PDF.
* **Auto-Logging:** Generates a fully styled `openpyxl` Excel tracker detailing the file name, revision, and the spatially extracted Code (color-coded in the Excel sheet for quick visual sorting).

### 2. Intelligent Nomenclature Engine (Folder & Archive Renamer)
* **Regex-Driven Standardization:** Automatically parses messy folder and archive names (`.zip`, `.rar`, `.7z`), strips out arbitrary spaces around hyphens, and formats the text into strict Title Case.
* **Smart Preservation:** Intelligently preserves data within brackets `()` or `[]` while standardizing the surrounding string to prevent data loss.
* **Dry Run Mode & Collision Prevention:** Features a 'Dry Run' simulation mode and collision detection to prevent accidental overwriting of identically named targets on case-insensitive file systems (like Windows).

## 🛠 Tech Stack & Architecture
* **PDF Vector Parsing:** `PyMuPDF` (`fitz`) for highly optimized, native document geometry and text-block coordinate extraction without OCR overhead.
* **GUI Framework:** `customtkinter` featuring a modern, multi-tabbed Dark Mode interface.
* **Data Export:** `openpyxl` for dynamic, formatted Excel generation with custom cell coloring and frozen panes.
* **Concurrency:** `threading` to keep the UI responsive during batch processing of massive directories.

## 📸 Interface Preview

![main-dashboard](main-dashboard.png)
