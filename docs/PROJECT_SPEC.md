# Image Quantization Utility
### Software Requirements Specification (SRS)

| Property | Value |
|---|---|
| Project name | Image Quantization Utility |
| Version | 1.0 |
| Status | Approved |
| Language | Python |
| Algorithm | K-Means Clustering |
| Initialization | K-Means++ |

## 1. Introduction

### 1.1 Purpose

The purpose of this project is to develop a Python-based image color quantization utility that reduces the number of distinct colors in digital images using unsupervised K-Means clustering.

The application will expose its functionality through two interfaces: a command-line interface (CLI) and a reusable Python API.

### 1.2 Problem Statement

Digital images can contain a large number of distinct RGB colors. By grouping similar colors into clusters and replacing individual pixel colors with representative cluster centroids, it is possible to produce visually similar images with a smaller color palette.

This project aims to implement this process efficiently while maintaining software quality, computational reliability and manageable memory consumption.

### 1.3 Objectives

- Implement K-Means and K-Means++ from scratch using NumPy.
- Develop a modular image-processing pipeline.
- Support both CLI and programmatic usage.
- Optimize numerical computation and memory consumption.
- Evaluate image quality and computational performance.
- Maintain professional software development practices.

## 2. Scope

### 2.1 In Scope

- JPEG and PNG input support.
- RGB color quantization.
- K-Means clustering with K-Means++ initialization.
- Configurable cluster count, iteration limit and random seed.
- CLI and Python API.
- Alpha-channel preservation.
- EXIF orientation correction.
- Chunked distance computation.
- PNG output.
- Automated testing and benchmarking.

### 2.2 Out of Scope for MVP

- GUI.
- Alternative clustering algorithms.
- CIELAB color space.
- GPU acceleration.
- Distributed processing.
- Web-based image processing.
- JPEG output encoding.

## 3. Technology Stack

| Component | Technology |
|---|---|
| Programming language | Python |
| Numerical computation | NumPy |
| Image processing | Pillow |
| CLI | argparse |
| Testing | pytest |
| Version control | Git and GitHub |
| Logging | Python logging |
| Benchmarking | time.perf_counter and memory profiling tools |

## 4. Functional Requirements

| ID | Requirement |
|---|---|
| FR-01 | Accept JPEG and PNG input images. |
| FR-02 | Accept an output destination. |
| FR-03 | Allow users to configure the number of clusters K. |
| FR-04 | Convert image pixels into RGB vectors. |
| FR-05 | Initialize centroids using K-Means++. |
| FR-06 | Assign pixels to their nearest centroid. |
| FR-07 | Recalculate cluster centroids iteratively. |
| FR-08 | Support convergence-based termination and a maximum iteration limit. |
| FR-09 | Reconstruct and save quantized images in PNG format. |
| FR-10 | Validate input files and algorithm parameters. |
| FR-11 | Support configurable random seeds. |
| FR-12 | Provide a command-line interface. |
| FR-13 | Provide a reusable Python API. |
| FR-14 | Preserve image dimensions and alpha transparency. |
| FR-15 | Normalize EXIF orientation before processing. |
| FR-16 | Implement chunked distance computation for memory management. |
| FR-17 | Handle empty clusters using a defined recovery strategy. |

## 5. Non-Functional Requirements

- NFR-01: Maintain readable, modular and maintainable code.
- NFR-02: Use vectorized NumPy operations for numerical computation.
- NFR-03: Avoid unnecessary Python-level loops over individual pixels.
- NFR-04: Manage memory consumption through chunked processing.
- NFR-05: Produce reproducible results with identical inputs and configurations.
- NFR-06: Provide meaningful error messages and diagnostic logging.
- NFR-07: Include automated unit and integration tests.
- NFR-08: Provide clear documentation for both interfaces.
- NFR-09: Support Windows, Linux and macOS where dependencies permit.

## 6. Input and Output Specifications

### Input

- Image file in JPEG or PNG format.
- Positive integer K representing the desired number of colors.
- Optional maximum iteration count.
- Optional convergence tolerance.
- Optional random seed.
- Optional processing configuration.

### Output

- Quantized PNG image.
- Preserved image dimensions.
- Preserved alpha channel when applicable.
- Execution information and diagnostic messages.

### Validation Constraints

- K must be positive.
- K must not exceed the number of distinct input RGB colors.
- The maximum iteration count must be positive.
- Input files must exist and be readable.
- Output destinations must be valid.

## 7. Algorithm Specifications

### 7.1 Color Representation

Represent each pixel as an RGB vector:

x = [R, G, B]

Each channel uses an 8-bit integer representation in the image, with suitable numerical conversion for clustering calculations.

### 7.2 Initialization

Use K-Means++ to select initial centroids probabilistically based on squared distances to the nearest previously selected centroid.

### 7.3 Assignment

Assign every pixel to its nearest centroid using squared Euclidean distance.

### 7.4 Centroid Update

Recalculate each centroid as the arithmetic mean of all RGB vectors assigned to that cluster.

### 7.5 Termination

Terminate when the configured convergence criterion is satisfied or the maximum iteration count is reached.

### 7.6 Memory Optimization

Process pixel-to-centroid distance calculations in configurable chunks to avoid unnecessarily large intermediate arrays.

### 7.7 Image Reconstruction

Replace every pixel with its assigned centroid color, convert the resulting values into a valid image representation and preserve the original alpha channel independently.

## 8. Acceptance Criteria

The MVP will be considered complete when:

1. JPEG and PNG inputs can be loaded successfully.
2. EXIF orientation is correctly normalized.
3. RGB quantization produces no more than K distinct colors.
4. Image dimensions remain unchanged.
5. Transparency is preserved for supported RGBA inputs.
6. K-Means++ initialization produces valid centroids.
7. The algorithm terminates within its configured iteration limit.
8. Repeated executions with identical configurations are reproducible.
9. Chunked processing produces results consistent with the unchunked reference implementation.
10. Invalid inputs are handled gracefully.
11. Both CLI and Python API work correctly.
12. Automated tests pass.

## 9. Testing and Evaluation

Testing will cover:

- Algorithm correctness.
- Image loading and reconstruction.
- Input validation.
- Edge cases and empty clusters.
- CLI integration.
- Python API integration.
- Reproducibility.
- Chunked versus unchunked numerical consistency.

Performance evaluation will consider:

- Execution time.
- Peak memory consumption.
- Image file-size reduction.
- Mean Squared Error (MSE).
- Peak Signal-to-Noise Ratio (PSNR).

Performance claims will be supported by reproducible benchmarks.

## 10. Future Enhancements

- Alternative initialization strategies.
- CIELAB color-space support.
- Configurable JPEG output.
- Advanced image-quality evaluation.
- Further memory optimization.
- Additional image formats.
- Python package distribution.
- Automated CI/CD workflows.

---

**End of Specification — Version 1.0**