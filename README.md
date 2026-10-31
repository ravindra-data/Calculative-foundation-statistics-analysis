# Linear Algebra Project: Students' Performance Analysis

A data-analysis project that applies **linear algebra** (vectors, matrices, geometry, eigenvalues) to a dataset of **600 students' scores across 6 subjects**. Everything is done practically in Python and explained theoretically in an accompanying PDF.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Folder Structure](#2-folder-structure)
3. [Dataset Description](#3-dataset-description)
4. [Requirements and Installation](#4-requirements-and-installation)
5. [How to Run](#5-how-to-run)
6. [Code Versions: Which One to Use](#6-code-versions-which-one-to-use)
7. [Task-to-Code Mapping](#7-task-to-code-mapping)
8. [Key Results](#8-key-results)
9. [Output Files](#9-output-files)
10. [Theory Document](#10-theory-document)
11. [Troubleshooting](#11-troubleshooting)
12. [Notes and Limitations](#12-notes-and-limitations)

---

## 1. Project Overview

**Problem statement:** A research institute has shared a dataset of students' performance scores across multiple subjects. As a data analyst, apply linear algebra techniques to:

1. Represent and manipulate data using vectors and matrices.
2. Perform advanced operations (dot products, cross products, vector projections, norms).
3. Interpret eigenvalues and eigenvectors to understand variance in the dataset.

**Main idea:** each student is a **vector** in 6-dimensional space (one axis per subject), and the whole class is a **600 × 6 matrix**. Relationships between subjects are studied through the **covariance matrix** and its **eigenvectors** (Principal Component Analysis).

---

## 2. Folder Structure

```
student_la_project/
│
├── README.md                         <- this file
├── requirements.txt                  <- Python packages needed
│
├── student_scores.csv                <- dataset (600 students x 6 subjects)
├── student_scores.xlsx               <- same dataset in Excel format
├── generate_dataset.py               <- script that created the dataset (reproducible)
│
├── simple_code.py                    <- Beginner: straight-line code, no functions
├── no_function_code.py               <- Intermediate: no functions, with checks and plots
├── intermediate_code.py              <- Intermediate: grouped into part-level functions
├── functions_code.py                 <- Intermediate: one small function per operation
├── linear_algebra_analysis.py        <- Advanced: full version with comments and extra analysis
│
├── Linear_Algebra_Theory_Concepts.pdf <- theory document with definitions (8 pages)
│
├── results_output.txt                <- saved console output of the advanced script
├── pca_plots.png                     <- scree plot, PC1 vs PC2 scatter, correlation heatmap
├── plane_3d.png                      <- best-fit plane in 3D
├── intermediate_plots.png            <- plots made by intermediate_code.py
└── no_function_plots.png             <- plots made by no_function_code.py
```

---

## 3. Dataset Description

| Property | Value |
|---|---|
| Files | `student_scores.csv`, `student_scores.xlsx` |
| Records | 600 students |
| Columns | 8 |
| Type | Synthetic (generated for learning purposes) |
| Random seed | 42 (regenerating gives the identical file) |

**Columns**

| Column | Description |
|---|---|
| `Student_ID` | Unique ID, `STU1001` to `STU1600` |
| `Name` | Randomly generated student name |
| `Maths` | Score out of 100 |
| `Physics` | Score out of 100 |
| `Chemistry` | Score out of 100 |
| `English` | Score out of 100 |
| `Computer_Science` | Score out of 100 |
| `Statistics` | Score out of 100 |

**How the data was generated:** scores are built from hidden "general ability", "quantitative ability" and "verbal ability" factors plus random noise, then rounded and clipped to 0-100. This makes Maths, Physics, Statistics and Computer Science strongly correlated, while English behaves more independently, which gives meaningful eigenvalue results.

**Summary statistics**

| Subject | Mean | Std. dev. | Min | Max |
|---|---|---|---|---|
| Maths | 67.52 | 9.45 | 38 | 96 |
| Physics | 63.92 | 9.89 | 36 | 92 |
| Chemistry | 65.90 | 8.89 | 40 | 94 |
| English | 69.23 | 10.03 | 43 | 100 |
| Computer_Science | 71.64 | 9.15 | 45 | 98 |
| Statistics | 64.65 | 9.60 | 37 | 100 |

To regenerate the dataset:

```bash
python generate_dataset.py
```

---

## 4. Requirements and Installation

- Python 3.8 or newer
- Packages: `numpy`, `pandas`, `matplotlib`, `openpyxl` (only needed for the `.xlsx` file)

```bash
pip install -r requirements.txt
```

---

## 5. How to Run

Keep all files in the same folder (the scripts read `student_scores.csv` from the folder they run in), then run **one** of the scripts:

```bash
python simple_code.py
python no_function_code.py
python intermediate_code.py
python functions_code.py
python linear_algebra_analysis.py
```

Run the scripts from inside the project folder so the CSV is found:

```bash
cd student_la_project
python no_function_code.py
```

---

## 6. Code Versions: Which One to Use

All versions produce the **same numerical results**. They differ only in style and depth.

| File | Level | Uses `def` functions | Comments | Plots | Best for |
|---|---|---|---|---|---|
| `simple_code.py` | Beginner | No | No | No | Learning the basic flow quickly |
| `no_function_code.py` | Intermediate | No | No | Yes | Step-by-step reading with checks and graphs |
| `intermediate_code.py` | Intermediate | Yes (per part) | No | Yes | Structured, reusable code |
| `functions_code.py` | Intermediate | Yes (per operation) | No | No | Seeing each operation as its own function |
| `linear_algebra_analysis.py` | Advanced | No | Yes | Yes (2 figures) | Full analysis, saves a results text file |

**Suggestion:** start with `simple_code.py` to understand the flow, then read `no_function_code.py` or `functions_code.py` for submission or viva.

---

## 7. Task-to-Code Mapping

| Task | What is computed | Where in the code |
|---|---|---|
| **Part A.1** | Each student as a vector in R^6 | Section "PART A" |
| **Part A.2a** | Norm-1 and Norm-2 | `np.sum(np.abs(u))`, `np.sqrt(np.sum(u**2))` |
| **Part A.2b** | Dot product and angle between two students | `np.dot`, `np.arccos` |
| **Part A.2c** | Cross product (Maths, Physics, Computer_Science) | `np.cross` |
| **Part A.3** | Projection of one vector onto another | `(u.v / v.v) * v` |
| **Part B.4** | Addition, multiplication, transpose, inverse, determinant | 6 x 6 blocks `A` and `B` |
| **Part C.5** | Line, plane and hyperplane fitted to the data | `np.polyfit`, `np.linalg.lstsq` |
| **Part C.6** | Dimensionality from 2D to 3D to higher | Dimension table, rank per subject count |
| **Part D.7** | Eigenvalues and eigenvectors of the covariance matrix | `np.linalg.eigh` |

**Why 6 x 6 blocks?** The full data matrix is 600 x 6 (not square), so it has no determinant or inverse. For Part B, `A` (students 1-6) and `B` (students 7-12) are used. The code also shows the square matrix `X^T X` and the pseudo-inverse for the full matrix.

---

## 8. Key Results

| Item | Result |
|---|---|
| Norm-1 / Norm-2 of student 1 | 423 / 172.84 |
| Dot product (student 1, student 2) | 25,420 |
| Angle between the two students | 7.45 degrees |
| Cross product (Maths, Physics, CS) | (-757, 393, 413) |
| Determinant of 6 x 6 block A | -8,391,734 (invertible, rank 6) |
| Best-fit line | Physics = 0.800 x Maths + 9.869 |
| Best-fit plane | CS = 0.485 x Maths + 0.295 x Physics + 20.092 |
| Trace of covariance matrix | 542.764 (equals sum of eigenvalues) |

**Eigenvalues and variance explained**

| Component | Eigenvalue | Variance explained | Cumulative |
|---|---|---|---|
| PC1 | 359.228 | 66.18% | 66.18% |
| PC2 | 85.244 | 15.71% | 81.89% |
| PC3 | 34.032 | 6.27% | 88.16% |
| PC4 | 26.814 | 4.94% | 93.10% |
| PC5 | 21.098 | 3.89% | 96.99% |
| PC6 | 16.349 | 3.01% | 100.00% |

**Interpretation**

- **PC1** has positive loadings on every subject, so it represents **overall academic ability**.
- **PC2** is dominated by English with the opposite sign to the quantitative subjects, so it represents **verbal vs. quantitative skill**.
- **PC1 + PC2 explain 81.89%** of the variance, so the 6-dimensional data can be reduced to 2 dimensions with little loss.

---

## 9. Output Files

| File | Created by | Contents |
|---|---|---|
| `results_output.txt` | `linear_algebra_analysis.py` | Full console output saved as text |
| `pca_plots.png` | `linear_algebra_analysis.py` | Scree plot, PC1 vs PC2 scatter, correlation heatmap |
| `plane_3d.png` | `linear_algebra_analysis.py` | Best-fit plane through (Maths, Physics, CS) |
| `intermediate_plots.png` | `intermediate_code.py` | Same three plots as the PCA figure |
| `no_function_plots.png` | `no_function_code.py` | Same three plots as the PCA figure |

Plot files are overwritten each time a script is run.

---

## 10. Theory Document

`Linear_Algebra_Theory_Concepts.pdf` (8 pages) explains every concept used in the project, with a definition box, formula and worked example for each:

1. Introduction: scalar, vector, matrix, and how they map to the dataset
2. Part A: norms, dot product and angle, cross product, projection
3. Part B: matrix addition, multiplication, transpose, determinant, inverse, rank
4. Part C: line, plane, hyperplane, dimensionality, linear transformation, least squares
5. Part D: mean, variance, covariance, eigenvalues, eigenvectors, PCA, interpretation
6. Summary table of results and a quick glossary

---

## 11. Troubleshooting

| Problem | Fix |
|---|---|
| `FileNotFoundError: student_scores.csv` | Run the script from inside the project folder, or keep the CSV next to the script |
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` |
| Plot window does not appear | Plots are saved as PNG files instead of being shown on screen |
| Eigenvector signs differ from the PDF | Signs are arbitrary (`v` and `-v` are both valid). The intermediate and advanced scripts flip them so PC1 loadings are positive; `simple_code.py` and `functions_code.py` do not, so PC1 appears negative there |
| Slightly different decimal values | Only display rounding differs, not the results |

---

## 12. Notes and Limitations

- The dataset is **synthetic**. It is meant to demonstrate the techniques, not to draw conclusions about real students.
- The cross product exists only in 3D, so it uses three selected subjects (Maths, Physics, Computer_Science).
- Determinant and inverse require a square matrix, so they are shown on a 6 x 6 block of the data, plus `X^T X` for the full matrix.
- Results shown here were produced with NumPy's `eigh` (for symmetric matrices) and `lstsq` (least squares).
