\# Flood Detection using Sentinel-1 SAR and Google Earth Engine (Python)



\---



\## 1. Introduction



Floods are one of the most frequent and damaging natural disasters, particularly in regions with extensive river systems such as Assam, India. Traditional optical satellite methods often fail during flood events due to heavy cloud cover.



This project implements a \*\*satellite-based flood detection pipeline\*\* using \*\*Sentinel-1 Synthetic Aperture Radar (SAR)\*\* data, which is capable of capturing surface conditions regardless of weather or daylight.



The system detects \*\*newly inundated areas\*\* by comparing temporal satellite observations and applies spatial filtering techniques to produce reliable flood maps.



\---



\## 2. Problem Statement



The objective is to:



\* Detect flood-affected regions using SAR imagery

\* Distinguish \*\*temporary flood water\*\* from permanent water bodies

\* Reduce speckle noise inherent in SAR data

\* Generate a clean flood mask

\* Estimate total flooded area in square kilometers



\---



\## 3. Study Area



\* \*\*Region:\*\* Assam, India

\* \*\*Coordinates:\*\* \[91, 25, 93, 27]

\* \*\*Geographical Characteristics:\*\*



&#x20; \* Dominated by Brahmaputra river basin

&#x20; \* High flood vulnerability due to flat terrain

&#x20; \* Seasonal monsoon flooding



\---



\## 4. Dataset Description



\### Sentinel-1 SAR Data



\* Source: Copernicus Open Access Hub

\* Dataset ID: `COPERNICUS/S1\_GRD`

\* Mode: Interferometric Wide Swath (IW)

\* Polarization: VV

\* Orbit: Descending



\### JRC Global Surface Water



\* Dataset: `JRC/GSW1\_4/GlobalSurfaceWater`

\* Used for masking permanent water bodies



\---



\## 5. Methodology



\### 5.1 Temporal Image Selection



Two time windows are selected:



\* \*\*Pre-flood period:\*\* June 1–15, 2022

\* \*\*Post-flood period:\*\* July 1–15, 2022



Median compositing is applied to reduce temporal noise.



\---



\### 5.2 SAR Backscatter Principle



In SAR imagery:



\* Water surfaces → \*\*low backscatter (dark pixels)\*\*

\* Land surfaces → \*\*higher backscatter\*\*



This difference is used for classification.



\---



\### 5.3 Noise Reduction



SAR images contain speckle noise. To mitigate this:



\* Apply \*\*focal mean filtering (30m radius)\*\*

\* Smooth local variations



\---



\### 5.4 Water Classification



A threshold-based approach is used:



\* Water condition:



```text

Backscatter < -17 dB

```



Outputs:



\* `before\_water`

\* `after\_water`



\---



\### 5.5 Flood Detection Logic



Flood is defined as:



```text

Flood = After Water AND NOT Before Water

```



This isolates \*\*newly formed water bodies\*\*, removing pre-existing water.



\---



\### 5.6 Permanent Water Removal



Using JRC dataset:



\* Pixels with >50% occurrence are treated as permanent water

\* These are excluded from flood detection



\---



\### 5.7 Spatial Filtering



To improve map quality:



\* \*\*Connected pixel filtering\*\*



&#x20; \* Removes isolated noise

\* \*\*Morphological smoothing\*\*



&#x20; \* Expands and connects nearby flood regions



\---



\### 5.8 Flood Area Estimation



Steps:



1\. Convert flood mask to area using `pixelArea()`

2\. Sum all pixels using `reduceRegion()`

3\. Convert to square kilometers



\---



\## 6. Results



\* \*\*Estimated Flood Area:\*\* \~550 sq km

\* \*\*Spatial Pattern Observed:\*\*



&#x20; \* Concentration along river channels

&#x20; \* Spread into adjacent floodplains

&#x20; \* Clusters near Brahmaputra basin



\---



\## 7. Output Visualization



The visualization displays:



\* Grayscale SAR background

\* Flooded regions highlighted in blue



Image: `output.png`



\---



\## 8. Technical Implementation



\### Core Libraries



\* Google Earth Engine API

\* Geemap

\* Python



\### Key Operations



\* ImageCollection filtering

\* Raster thresholding

\* Logical masking

\* Morphological operations

\* Regional reduction



\---



\## 9. Performance Considerations



\* Computation performed on Google Earth Engine cloud

\* Efficient handling of large-scale satellite datasets

\* Scale parameter (30m) balances:



&#x20; \* Accuracy

&#x20; \* Computational cost



\---



\## 10. Limitations



\* Threshold-based classification may:



&#x20; \* Misclassify wet soil as water

&#x20; \* Miss shallow flooding

\* SAR shadow effects in hilly terrain

\* No validation with ground-truth data



\---



\## 11. Future Work



\* Integrate \*\*NDVI\*\* for vegetation damage analysis

\* Apply \*\*DEM-based masking\*\* to remove slope-induced errors

\* Use \*\*machine learning classification models\*\*

\* Add \*\*multi-date flood progression tracking\*\*

\* Build \*\*interactive dashboard for disaster response\*\*



\---



\## 12. Reproducibility



\### Installation



```bash

pip install earthengine-api geemap

```



\---



\### Authentication



```python

import ee

ee.Authenticate()

ee.Initialize()

```



\---



\### Execution



Run the notebook:



```bash

jupyter notebook

```



Open:



```

flood\_detection.ipynb

```



\---



\## 13. Repository Structure



```text

Flood-Detection-GEE/

│── flood\_detection.ipynb

│── output.png

│── requirements.txt

│── README.md

```



\---



\## 14. Key Contributions



\* End-to-end SAR-based flood detection pipeline

\* Noise-robust flood extraction method

\* Automated flood area estimation

\* Cloud-based geospatial analysis using GEE



\---



\## 15. Author



Shivani Negi

GitHub: https://github.com/kmshivani05



\---



\## 16. References



\* ESA Sentinel-1 Mission

\* Google Earth Engine Documentation

\* JRC Global Surface Water Dataset



\---



