\# Flood Detection using Sentinel-1 SAR and Google Earth Engine (Python)



\---



\## 1. Introduction



Floods are among the most destructive natural disasters, especially in regions like Assam, India where river systems overflow during monsoon seasons. Optical satellite imagery often fails due to cloud cover during such events.



This project uses \*\*Sentinel-1 SAR (Synthetic Aperture Radar)\*\* data, which can penetrate clouds and capture surface conditions in all weather, to detect flood-affected areas accurately.



\### Output Preview



!\[Flood Detection Output](output.png)



The blue regions represent \*\*detected flood areas\*\*, primarily concentrated along river basins and low-lying floodplains.



\---



\## 2. Problem Statement



The goal of this project is to:



\* Detect flood-affected areas using SAR imagery

\* Identify \*\*new water bodies formed after flooding\*\*

\* Remove permanent water bodies

\* Reduce SAR noise (speckle effect)

\* Estimate total flooded area (in sq km)



\---



\## 3. Study Area



\* \*\*Region:\*\* Assam, India

\* \*\*Coordinates:\*\* \[91, 25, 93, 27]

\* \*\*Characteristics:\*\*



&#x20; \* Brahmaputra river basin

&#x20; \* High flood vulnerability

&#x20; \* Flat terrain with seasonal inundation



\---



\## 4. Dataset Used



\### Sentinel-1 SAR



\* Dataset: `COPERNICUS/S1\_GRD`

\* Mode: IW (Interferometric Wide Swath)

\* Polarization: VV

\* Orbit: DESCENDING



\### Surface Water Dataset



\* Dataset: `JRC/GSW1\_4/GlobalSurfaceWater`

\* Purpose: Remove permanent water bodies



\---



\## 5. Methodology



\### 5.1 Time Selection



\* Before flood: June 1–15, 2022

\* After flood: July 1–15, 2022



Median images are computed to reduce temporal noise.



\---



\### 5.2 SAR-Based Water Detection



\* Water appears \*\*dark\*\* in SAR (low backscatter)

\* Land appears \*\*brighter\*\*



Threshold used:



```text

Backscatter < -17 dB → Water

```



\---



\### 5.3 Flood Extraction



Flood is defined as:



```text

Flood = After Water AND NOT Before Water

```



This ensures only \*\*newly flooded regions\*\* are captured.



\---



\### 5.4 Permanent Water Removal



Using JRC dataset:



\* Pixels with >50% water occurrence are removed

\* Ensures lakes and rivers are excluded



\---



\### 5.5 Noise Reduction



\* Focal mean filter applied

\* Connected pixel filtering removes small noisy patches

\* Morphological smoothing improves spatial continuity



\---



\### 5.6 Flood Area Calculation



\* Pixel area computed using `pixelArea()`

\* Summed using `reduceRegion()`

\* Converted to square kilometers



\---



\## 6. Results



\* \*\*Estimated Flood Area:\*\* \~550 sq km

\* Flood distribution observed:



&#x20; \* Along river channels

&#x20; \* Across floodplains

&#x20; \* Near low elevation zones



\---



\## 7. Visualization



\* Grayscale: SAR imagery

\* Blue overlay: Flooded areas

\* Clear clustering near Brahmaputra river basin



\---



\## 8. Tech Stack



\* Python

\* Google Earth Engine API

\* Geemap



\---



\## 9. How to Run



\### Install Dependencies



```bash

pip install earthengine-api geemap

```



\---



\### Authenticate



```python

import ee

ee.Authenticate()

ee.Initialize()

```



\---



\### Run Notebook



```bash

jupyter notebook

```



Open:



```

flood\_detection.ipynb

```



\---



\## 10. Project Structure



```

Flood-Detection-GEE/

│── flood\_detection.ipynb

│── output.png

│── requirements.txt

│── README.md

```



\---



\## 11. Limitations



\* Threshold-based detection may misclassify wet soil

\* No ground truth validation

\* SAR shadow effects in hilly regions



\---



\## 12. Future Improvements



\* NDVI-based vegetation damage analysis

\* DEM-based terrain correction

\* Machine learning flood classification

\* Multi-date flood progression mapping

\* Web dashboard for real-time monitoring



\---



\## 13. Key Highlights



\* Uses SAR for all-weather flood detection

\* Efficient large-scale processing with GEE

\* Clean flood extraction using logical masking

\* Accurate area estimation



\---



\## 14. Author



Shivani Negi

GitHub: https://github.com/kmshivani05



\---



\## 15. References



\* Sentinel-1 SAR (ESA)

\* Google Earth Engine Docs

\* JRC Global Surface Water



\---



