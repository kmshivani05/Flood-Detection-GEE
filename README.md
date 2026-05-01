\# Flood Detection using Sentinel-1 SAR and Google Earth Engine (Python)



\---



\## 1. Introduction



Floods are among the most destructive natural disasters, especially in regions like Assam, India where river systems overflow during monsoon seasons. Optical satellite imagery often fails due to cloud cover during such events.



This project uses \*\*Sentinel-1 SAR (Synthetic Aperture Radar)\*\* data, which can penetrate clouds and capture surface conditions in all weather, to detect flood-affected areas accurately.



\### Output Preview



<p align="center">

&#x20; <img src="./output.png" width="650"/>

</p>



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

&#x20; \* Flat terrain



\---



\## 4. Dataset Used



\### Sentinel-1 SAR



\* Dataset: `COPERNICUS/S1\_GRD`

\* Mode: IW

\* Polarization: VV

\* Orbit: DESCENDING



\### Surface Water Dataset



\* Dataset: `JRC/GSW1\_4/GlobalSurfaceWater`

\* Used to remove permanent water



\---



\## 5. Methodology



\### Time Selection



\* Before flood: June 1–15, 2022

\* After flood: July 1–15, 2022



Median composites are used to reduce noise.



\---



\### Water Detection



Water in SAR appears dark (low backscatter):



```text

Backscatter < -17 dB → Water

```



\---



\### Flood Extraction



```text

Flood = After Water AND NOT Before Water

```



This captures only \*\*new flood regions\*\*.



\---



\### Permanent Water Removal



\* Pixels with >50% water occurrence removed

\* Ensures rivers/lakes are excluded



\---



\### Noise Reduction



\* Focal mean filtering

\* Connected pixel filtering

\* Morphological smoothing



\---



\### Area Calculation



\* Pixel area → `pixelArea()`

\* Summation → `reduceRegion()`

\* Converted to sq km



\---



\## 6. Results



\* \*\*Estimated Flood Area:\*\* \~550 sq km



\### Observations:



\* Flood clusters along river channels

\* Spread into surrounding plains

\* Dense concentration near Brahmaputra basin



\---



\## 7. Visualization



\* Grayscale → SAR imagery

\* Blue overlay → Flooded regions



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



\### Run



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



\* Threshold method may misclassify wet soil

\* No ground truth validation

\* SAR shadow issues in hilly regions



\---



\## 12. Future Improvements



\* NDVI-based flood impact analysis

\* DEM-based correction

\* ML-based classification

\* Time-series flood tracking

\* Interactive dashboard



\---



\## 13. Highlights



\* Works in all weather conditions (SAR)

\* Cloud-based large-scale processing

\* Clean flood extraction pipeline

\* Accurate area estimation



\---



\## 14. Author



\*\*Shivani Negi\*\*

GitHub: https://github.com/kmshivani05



\---



\## 15. References



\* ESA Sentinel-1

\* Google Earth Engine Docs

\* JRC Global Surface Water



\---



