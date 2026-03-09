# Raman-Extraction-Tool: Digitizing Spectra from Literature figure
A Python-based pipeline for digitizing and standardizing Raman spectra from published figures. Features automated color masking, IModPoly baseline correction, and physical axis mapping to create AI-ready spectral databases.

This structure highlights the improvements over existing workflows, such as the M Terán et al. (2025) study (https://doi.org/10.1016/j.chemolab.2025.105476) as our referenced.
The study used contour detection to localize traces and the airPLS algorithm for baseline removal, but we implemented color masking to isolate the spectrum and the IModPoly (Improved Modified Multi-Polynomial) algorithm for baseline correction. Additionally, instead of using peak detection to find axis ticks, the code employs a direct linear mapping function (pixel_to_unit) to assign wavenumbers to pixel coordinates. Moreover, we still using Tesseract OCR for label identification, applying a Savitzky-Golay filter for smoothing, and standardizing the final output to a 450–1800 cm⁻¹ range with 1 cm⁻¹ steps through linear interpolation and min-max normalization.

This repository provides an automated workflow to extract numerical data from Raman spectrum images found in published articles and process them into a standardized format for database inclusion.

# Key features

## 1.Targeted Extraction: 
Uses Color Masking to isolate the spectrum line from complex backgrounds, offering a more precise alternative to standard contour detection.

## 2.Advanced Baseline Correction: 
Implements the IModPoly (Improved Modified Multi-Polynomial) algorithm to flatten baselines and correct image tilt.

## 3.Direct Axis Mapping: 
Employs a pixel_to_unit linear mapping function for high-accuracy wavenumber assignment instead of relying solely on peak detection.

## 4.Standarization:
> - Smoothed to reduce noise
> - Baseline removed
> - Interpolated to minimum 450-1800 cm⁻¹ with a step of 1 cm⁻¹
> - Min-max normalized
>

# How to extraction
## 1.Image Loading: 
Pre-processes target images using OpenCV.

## 2.Coordinate Extraction: 
Identifies (x, y) coordinates via masking and applies a median filter to handle noise and overlapping pixels.

## 3.Physical Calibration: 
Converts pixel coordinates to physical units (Wavenumber/Intensity).

## 4.Signal Processing:
  - Smoothing: Savitzky-Golay filter.

  - Baseline Removal: IModPoly algorithm.

  - Normalization: Min-Max scaling (0.0 to 1.0).

## 5.Export: 
Generates interactive Plotly visualizations and exports a two-column CSV (Wavenumber, Intensity).
