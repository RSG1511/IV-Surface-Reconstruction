# IV Surface Reconstruction for NIFTY50 Options

## Overview
This project reconstructs missing Implied Volatility (IV) values in a NIFTY50 options dataset.
The objective is to accurately estimate missing IV observations while preserving the structure of the implied volatility surface and avoiding look-ahead bias.
The solution was developed as part of a quantitative finance challenge focused on volatility surface reconstruction.
## Problem Statement
The dataset contains:
* Timestamp-wise option market observations
* Underlying asset prices
* Implied volatilities for multiple call (CE) and put (PE) strikes

A subset of IV values is intentionally removed.
The task is to reconstruct these missing values as accurately as possible.

## Financial Intuition

Implied volatility surfaces exhibit strong local structure:
* Nearby strikes tend to have similar IV values.
* Volatility smiles evolve smoothly across strikes.
* Call and Put surfaces often have different skews.
* Local strike information is often more informative than distant observations.

Therefore, the reconstruction problem is approached as a local surface estimation problem rather than a generic machine learning task.

## Methodology
### 1. Separate Call and Put Surfaces
Call (CE) and Put (PE) strikes are reconstructed independently to preserve their distinct volatility structures.

### 2. Local Strike Neighborhood
For each missing IV value:
* Identify the nearest available strikes.
* Construct a local neighborhood using nearby observed IV values.

### 3. Local Interpolation
Missing IV values are estimated using local interpolation within the strike neighborhood.

This preserves:
* Surface smoothness
* Volatility smile structure
* Local strike relationships

### 4. Edge Handling
Boundary strikes are reconstructed using slope-based extrapolation to avoid unrealistic distortions near the edges of the surface.

### 5. No Look-Ahead Bias

The model never uses:
* Future timestamps
* Future IV observations
* Backward filling from future data
Only information available at the current timestamp is used.
