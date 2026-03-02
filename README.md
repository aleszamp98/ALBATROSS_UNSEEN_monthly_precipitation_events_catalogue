## Catalogue of simulated high-intensity monthly precipitation events for Kumasi Hub and Keta Basin Hub 

### Short introduction: 
This dataset presents a catalogue of simulated monthly means of daily precipitation rates based on a locally-validated seasonal forecast system for the Kumasi Hub and the Keta Basin Hub. The catalogue is based on a "reforecast ensemble pooling" methodology, which relies on extracting unprecedented events from large ensembles of dynamical seasonal forecasts. 
The method processes total precipitation outpt from the ECMWF SEAS5 full ensemble reforecasts spanning the 1993–2016 period across all available lead times. The extraction is conditioned on a statistical validation framework, comprising independence, stability, and fidelity tests, against observational dataset (GPCP). Only the specific initialization months and lead times that successfully pass all statistical criteria are retained in the final catalogue and assigned a unique identifier. 
The resulting validated dataset, through the provided unique identifiers, facilitates the retrieval of supplementary atmospheric variables from the Copernicus Climate Data Store to charaterize high-intensity precipitation events. 

### What is this?
This catalogue is provided as a tabular dataset containing simulated monthly means of daily precipitation rates based on a locally-validated seasonal forecast system for the Kumasi Hub and the Keta Basin Hub, focusing on the months of May and June (Ghana’s rainy season). The dataset is generated using the "reforecast ensemble pooling" methodology ​(Thompson et al., 2017)​ applied to the ECMWF SEAS5 full ensemble dynamical seasonal forecasts (1993–2016), incorporating all six available lead times. 

Each entry in the catalogue represents a specific event and includes:
- The monthly averaged daily precipitation rate, simulated at the model grid point closest to the Kumasi Hub, in units (mm/day). 
- The estimated return period of the event, expressed in (years). 
- A unique identifier (unseen_id) specifying the initialization month, the ensemble member, and the reference date. 

Raw ECMWF SEAS5 total precipitation rate data for all initialization months (1993–2016) were retrieved from the Copernicus Climate Change Service (C3S) Climate Data Store (CDS) (https://cds.climate.copernicus.eu/). To ensure the reliability of the UNSEEN (Unprecedented Simulated Extremes Using Ensembles) extraction, the dataset underwent statistical validation as described in  (Buccellato et al., 2026; Kelder et al., 2022)  . Three tests were performed on the May and June data across different lead times: independence, stability and fidelity tests. 

Only simulated values corresponding to months and specific lead times that passed all three statistical tests were retained. Consequently, each validated month and lead time combination provides 25 independent observations, corresponding to the different ensemble members. 

The return period for each event was calculated as the reciprocal of its total precipitation rate rank, relative to all pooled events for that specific month. 

Each catalogue entry is assigned a unique identifier formatted as init_MM-member_NN-date_YYYY-MM  (Bianco et al., 2026)  . For instance, "init_03-member_15-date_2007-06" indicates a precipitation rate occurring in June 2007, simulated by the 16th ensemble member (indexed 0 to 24), from a forecast initialized in March. 

This ID allows users to trace the origin of a specific high-intensity event. It can be used to query the C3S CDS and download additional atmospheric variables (e.g. geopotential height fields) associated with that exact ensemble member and initialization period, enabling an augmented physical description of the high-intensity event. 

For each month, the catalogue groups the top 100 events with the highest return periods for monthly-averaged daily precipitation rates, sorted in descending order. The months are presented chronologically (e.g., June entries follow May entries). 

### Who Is This For?
Intended users: researchers in the area of climate predictions and risk assessment, hydrologists, post-graduate students   

Required experience level:  Basic Python programming skills and basic understanding of seasonal forecasting systems, meteorological variables and return period concepts. 

### What Can You Use It For? 
This validated dataset enables the detection and characterization of high-intensity precipitation events over the Kumasi Hub. Through the provided unique identifiers (unseen_id), it facilitates the retrieval of supplementary atmospheric variables from the Copernicus Climate Data Store (C3S CDS). This enables users to reconstruct the conditions generating specific unprecedented high-intensity events. Additionally, the catalogue supports the estimation of extended return periods for regional climate risk assessment. 

### How to Get Started:
The dataset is provided as a standard .csv file. It can be inspected using programming languages, spreadsheet applications, or basic text editors. The dataset uses a colon (,) as the column delimiter. 

##### Option 1: Using Python 
To load and analyze the dataset, simple Python scripts with the pandas library can be used. Ensure pandas is installed (e.g., via pip install pandas) before running the following script: 
```
import pandas as pd  
file_path = 'path/to/your/UNSEEN_Kumasi_top100.csv'  
df = pd.read_csv(file_path, sep=';') 
print(df.head())
``` 

##### Option 2: Using Spreadsheet Software 
The dataset can be inspected using standard software such as Microsoft Excel, Google Sheets, or OpenOffice Calc. To prevent tabular formatting errors during the import process, ensure you explicitly set the custom separator/delimiter to a semicolon (;). 

##### Option 3: Using a Text Editor  
For a quick inspection of the raw data, the file can be opened directly with any standard text editor (e.g., Notepad on Windows, standard Text Editors on Linux/macOS). 



### Notes:
Details about the three statistical tests performed to select reforecast ensemble pooled monthly means: 
- Independence Test: Evaluates the assumption that individual ensemble members are statistically independent. For each month and lead time, pooled along the 24-year axis, the Spearman rank correlation coefficient was computed across all 300 possible pairs of the 25 ensemble members. The resulting distribution was compared against a reference distribution generated from synthetic, uncorrelated gamma-distributed time series of the same length. The test is passed if the median of the correlation coefficients falls within the interquartile range (IQR) of the independent distribution. 
- Stability Test: Assesses the potential influence of model drift at increasing lead times. The median of the precipitation distribution for a given lead time is compared with the IQRs of the distributions at the previous and subsequent lead times. The test is passed if the median falls within both IQRs. 
- Fidelity Test: Evaluates the similarity between simulations and observations using higher-order statistical moments (standard deviation, skewness, and kurtosis). The Global Precipitation Climatology Project (GPCP) monthly dataset was used as the observational baseline (https://psl.noaa.gov/data/gridded/data.gpcp.html). 1,000 proxy time series were bootstraped for each month to replicate the 24-year forecast period and the statistical moments for each series were computed. The test is passed if the observed moments fall within the acceptance range of the bootstrapped distributions. 

### Authors' Contacts:
- Alessandro Zampella, University of Bologna, alessandro.zampella2@unibo.it 
- Paolo Ruggieri, University of Bologna 
- Laura Sandra Leo, University of Bologna

### References
- ​​Bianco, E., Davini, P., Zappa, G., Manzato, A., Giordani, A., & Ruggieri, P. (2026). A framework for generating catalogues of high-impact UNSEEN flood events. Climate Services, 42, 100636. https://doi.org/10.1016/j.cliser.2026.100636
​- Buccellato, M., Ruggieri, P., & Porcù, F. (2026). Seasonal hindcasts to assess the hazard of meteorological drought over Europe: A multimodel approach. Quarterly Journal of the Royal Meteorological Society. https://doi.org/10.1002/qj.70076
- ​Kelder, T., Marjoribanks, T. I., Slater, L. J., Prudhomme, C., Wilby, R. L., Wagemann, J., & Dunstone, N. (2022). An open workflow to gain insights about low‐likelihood high‐impact weather events from initialized predictions. Meteorological Applications, 29(3). https://doi.org/10.1002/met.2065 
- ​Thompson, V., Dunstone, N. J., Scaife, A. A., Smith, D. M., Slingo, J. M., Brown, S., & Belcher, S. E. (2017). High risk of unprecedented UK rainfall in the current climate. Nature Communications, 8(1), 107. https://doi.org/10.1038/s41467-017-00275-3 
