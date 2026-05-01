\# Flood Detection using Google Earth Engine (Python)



\## Overview



This project detects flood-affected areas using Sentinel-1 SAR satellite data. It compares pre-flood and post-flood imagery to identify newly inundated regions and estimate total flood extent.



\---



\## Methodology



\* Sentinel-1 SAR data (VV polarization) is used

\* Pre-flood and post-flood images are processed

\* Backscatter thresholding identifies water bodies

\* Permanent water is removed using JRC Global Surface Water dataset

\* Noise is reduced using connectivity filtering

\* Spatial smoothing is applied for continuous flood regions

\* Flood area is calculated using pixel area



\---



\## Results



\* Estimated Flood Area: \*\*\~550 sq km\*\*

\* Region: Assam, India

\* Flood areas are clearly visible along river basins and nearby plains



\---



\## Output Visualization



!\[Flood Map](./output.png)



\---



\## Tech Stack



\* Python

\* Google Earth Engine API

\* Geemap



\---



\## How to Run



1\. Install dependencies:



&#x20;  ```

&#x20;  pip install earthengine-api geemap

&#x20;  ```



2\. Authenticate:



&#x20;  ```

&#x20;  import ee

&#x20;  ee.Authenticate()

&#x20;  ee.Initialize()

&#x20;  ```



3\. Run the script:



&#x20;  ```

&#x20;  python flood\_detection.py

&#x20;  ```



\---



\## Key Learnings



\* SAR-based flood detection using backscatter analysis

\* Handling noise in satellite imagery

\* Spatial filtering and smoothing techniques

\* Working with Google Earth Engine in Python



\---



\## Future Improvements



\* Integrate NDVI to assess vegetation damage

\* Use machine learning for improved classification

\* Add multi-date flood progression analysis



\---



\## Author



Shivani Negi

