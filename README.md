# EnergyBench
EnergyBench: A Large-Scale Energy Meter Dataset and Benchmark for Load Forecasting

## Overview
Energy data analytics is crucial for optimizing energy consumption, improving operational efficiency, and supporting sustainability in power systems. Despite its importance, the lack of large-scale, diverse, and publicly available energy datasets poses a significant challenge for training and evaluating advanced AI models. To address this, we introduce **EnergyBench**, a comprehensive dataset designed to support **Short-Term Load Forecasting (STLF)** and to support a variety of energy analytics applications, including load profile analysis, and load forecasting. EnergyBench comprises a real-world subset containing **78,037** electricity time series from commercial and residential buildings across the globe, with sampling intervals ranging from 15 minutes to 1 hour, and a synthetic subset of 120 million building time series generated using energy simulation models. 

Along with the dataset , we also benchmark a variety of traditional and foundation models for STLF and analyze their performance across different regions.
We provide an Hugging Face Dataset for multiple real building and synthetic energy consumption datasets as Pandas DataFrames in Parquet, simple (naive) to advanced (TSFM) baselines, metrics management, and more.

## Getting Started
We recommend using [Anaconda](https://www.anaconda.com/download) to run the experiments. Create the separate conda environment using the (modelname)_environment.yml found
under each model directory in the Notebooks. 
```
conda env create -f <modelname>_environment.yml
```
For TimesFM, kindly follow the respective [READEME.md](https://github.com/google-research/timesfm/blob/master/README.md) for the installation. For more information about each model, kindly look in 
their Github repositories.

## Benchmarking
**STLF**:

The univariate short-term load forecasting (STLF) problem can be defined
as follows: Given *H* past load values *x*<sub>*t* − *H* : *t*</sub>, we
aim to predict the conditional distribution of *T* unobserved future
load values *y*<sub>*t* + 1 : *t* + *T*</sub>. For our analysis, we
considered the STLF problem of forecasting the next day’s load values (T
= 24) using data from the past week (H = 168).

**Protocol**:
- We evaluate a range of models on our real 69,560 residential buildings, from simple baseline statistical models to advanced TSFM under a zero-shot setting for STLF.
- To enusre the fair comparison, we have used only real residential buildings, since some of the real commercial buildings have been included in the pre-training corpora of existing open-source TSFMs.
- Also, it is to be noted that, all real residential buildings, except LCL, in our EnergyBench have not been included in the pre-training datasets of existing open-source TSFMs.
- This highlights the potential of EnergyBench as a valuable resource for evaluating generalization and transfer capabilities of TSFMs across previously unseen building energy consumption domains

**Evaluation metrics**:
- NRMSE - Normalized Root Mean Squared Error (%)

## Dataset Repository
EnergyBench is hosted in the Hugging Face and is available for download with a permissive CC-4.0 license.
[HuggingFace Datasets](https://huggingface.co/datasets/ai-iot/EnergyBench)

## Overview of Dataset

It compiles over 60 detailed electricity consumption datasets encompassing approximately 78,037 real buildings representing the global building stock, offering insights into the temporal and spatial variations in energy consumption. The buildings are classified into two categories: Commercial, which includes **2,916** buildings, and Residential, which includes **75,121** buildings, with a total of 65,000 building-days of time-series data. These buildings span diverse geographies, climatic zones, and operational profiles, providing a broad spectrum of usage patterns. Additional to the real buildings, it also includes synthetic and simulated buildings electricity consumption data.

All processed datasets contain hourly data, with some offering additional 15-minute and 30-minute resolution. To ensure efficient storage, we saved the datasets in Parquet format rather than CSV. For datasets involving a large number of buildings, we partitioned the data into multiple Parquet files.

Table 1: Summary of EnergBench dataset (Real Buildings)

| Category    | # Datasets | # Buildings | # Days | # Hourly Obs |
|-------------|-------------|--------------|---------|--------|
| Commercial  | 20          | 2,916        | 16,706  | 62M    |
| Residential | 47          | 75,121       | 43,852  | 1.2B   |

Table 2: Summary of EnergBench dataset (Synthetic and Simulated Buildings)

| Category    | # Datasets | # Buildings | # Days | # Hourly Obs |
|-------------|-------------|--------------|---------|--------|
| Commercial  | 1           | 207,559      | 365     | ~1.7B  |
| Residential | 4           | ~120M        | 966     | ~1044B |

### Commercial Datasets:

* **BDG-2:** An open-access dataset comprising time-series data from **1,578 buildings** in the **USA**. The dataset spans from **January 1, 2016, to December 31, 2017 (730 days)**, with an **hourly processed resolution** capturing electricity usage and other system activities. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/BDG-2_data_quality_heatmap.png" target="_blank">BDG-2 Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/BDG-2_weather_sensitivity_heatmap.png" target="_blank">BDG-2 Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/BDG-2_Breakout_Heatmap.png" target="_blank">BDG-2 Breakout Heatmap</a></li></ul>
        </details>
    
* **Berkely:** Includes energy consumption data for **one office building** in **Berkeley, California**, recorded from **January 1, 2018, to January 1, 2021 (1,096 days)**. Data was processed at both **15-minute and 1-hour resolutions**. (CC0 1.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/Berkely_data_quality_heatmap.png" target="_blank">Berkely Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/Berkely_weather_sensitivity_heatmap.png" target="_blank">Berkely Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/Berkely_Breakout_Heatmap.png" target="_blank">Berkely Breakout Heatmap</a></li></ul>
        </details>
    
* **BPDB:** Collected from **one building** in **Bangladesh**, this dataset spans from **January 1, 2018, to April 30, 2023 (1,945 days)**. It features a source and processed resolution of **1-day**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/BPDB_data_quality_heatmap.png" target="_blank">BPDB Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/BPDB_weather_sensitivity_heatmap.png" target="_blank">BPDB Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/BPDB_Breakout_Heatmap.png" target="_blank">BPDB Breakout Heatmap</a></li></ul>
        </details>

* **CU-BEMS:** Includes data from **one smart building** in **Thailand** recorded from **July 1, 2018, to December 31, 2019 (548 days)**. Originally recorded at 1-minute intervals, it was processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/CU-BEMS_data_quality_heatmap.png" target="_blank">CU-BEMS Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/CU-BEMS_weather_sensitivity_heatmap.png" target="_blank">CU-BEMS Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/CU-BEMS_Breakout_Heatmap.png" target="_blank">CU-BEMS Breakout Heatmap</a></li></ul>
        </details>
    
* **DGS:** Includes energy consumption data from **322 commercial buildings** in the **USA**, spanning from **January 3, 2016, to December 2, 2018 (1,064 days)**. The processed resolution is **15-minute and 1-hour**. (MIT License)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/DGS_data_quality_heatmap.png" target="_blank">DGS Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/DGS_weather_sensitivity_heatmap.png" target="_blank">DGS Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/DGS_Breakout_Heatmap.png" target="_blank">DGS Breakout Heatmap</a></li></ul>
        </details>
    
* **EnerNOC:** Comprises anonymized data for **100 commercial and industrial sites** across the **USA**, covering **January 1, 2012, to January 1, 2013 (366 days)**. Source data at 5-minute intervals was processed to **5-minute, 15-minute, and 1-hour resolutions**. (Creative Commons Attribution-NonCommercial 3.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/Enernoc_data_quality_heatmap.png" target="_blank">EnerNOC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/Enernoc_weather_sensitivity_heatmap.png" target="_blank">EnerNOC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/Enernoc_Breakout_Heatmap.png" target="_blank">EnerNOC Breakout Heatmap</a></li></ul>
        </details>
    
* **EWELD:** Contains electricity consumption from **386 industrial and commercial users** in **Southern China** across 17 industries. It spans from **June 2, 2016, to August 10, 2022 (2,260 days)**, with a processed resolution of **15-minute and 1-hour**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/EWELD_data_quality_heatmap.png" target="_blank">EWELD Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/EWELD_weather_sensitivity_heatmap.png" target="_blank">EWELD Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/EWELD_Breakout_Heatmap.png" target="_blank">EWELD Breakout Heatmap</a></li></ul>
        </details>
    
* **HB:** Includes energy consumption for **one hospital building** in **Phoenix, USA**, covering the full year of **2023 (January 1 to December 31; 364 days)** at an **hourly resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/HB_data_quality_heatmap.png" target="_blank">HB Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/HB_weather_sensitivity_heatmap.png" target="_blank">HB Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/HB_Breakout_Heatmap.png" target="_blank">HB Breakout Heatmap</a></li></ul>
        </details>
    
* **I-Blend:** Contains electrical energy data from **9 campus-scale buildings** in **India** from **August 10, 2013, to December 31, 2017 (1,604 days)**. Processed resolutions include **1-minute, 15-minute, and 1-hour**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/Iblend_data_quality_heatmap.png" target="_blank">I-Blend Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/IBlend_weather_sensitivity_heatmap.png" target="_blank">I-Blend Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/IBlend_Breakout_Heatmap.png" target="_blank">I-Blend Breakout Heatmap</a></li></ul>
        </details>
    
* **IOT:** Collected from **one building** at the **University of Sharjah** from **January 1, 2024, to June 20, 2024 (171 days)**. Data was processed from a 12-hour source resolution to a **daily resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/IOT_data_quality_heatmap.png" target="_blank">IOT Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/IOT_weather_sensitivity_heatmap.png" target="_blank">IOT Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/IOT_Breakout_Heatmap.png" target="_blank">IOT Breakout Heatmap</a></li></ul>
        </details>
    
* **IPC-Commercial:** Includes electricity consumption for **3 buildings** within an industrial park in **China** from **January 1, 2016, to December 31, 2021 (2,191 days)** at an **hourly resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/IPC_data_quality_heatmap.png" target="_blank">IPC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/IPC-Commercial_weather_sensitivity_heatmap.png" target="_blank">IPC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/IPC-Commercial_Breakout_Heatmap.png" target="_blank">IPC Breakout Heatmap</a></li></ul>
        </details>
    
* **NEST-Commercial:** Open building data from **one building** in **Switzerland** recorded from **July 1, 2019, to June 30, 2023 (1,460 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/NEST_data_quality_heatmap.png" target="_blank">NEST Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/NEST-Commercial_weather_sensitivity_heatmap.png" target="_blank">NEST Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/NEST-Commercial_Breakout_Heatmap.png" target="_blank">NEST Breakout Heatmap</a></li></ul>
        </details>
    
* **PSS:** Data from **53 buildings** in the **Western Cape, South Africa**, spanning **December 1, 2022, to November 30, 2023 (364 days)** with **30-minute and 1-hour processed resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/PSS_data_quality_heatmap.png" target="_blank">PSS Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/PSS_weather_sensitivity_heatmap.png" target="_blank">PSS Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/PSS_Breakout_Heatmap.png" target="_blank">PSS Breakout Heatmap</a></li></ul>
        </details>
    
* **SEWA:** Provided by the Sharjah Electricity and Water Authority, this data from **one site** in the **UAE** spans **January 1, 2020, to December 31, 2021 (730 days)** at an **hourly resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/SEWA_data_quality_heatmap.png" target="_blank">SEWA Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/SEWA_weather_sensitivity_heatmap.png" target="_blank">SEWA Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/SEWA_Breakout_Heatmap.png" target="_blank">SEWA Breakout Heatmap</a></li></ul>
        </details>
    
* **SKC:** Contains data from **10 manufacturing factories** in **South Korea** from **March 1, 2019, to September 30, 2019 (213 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/SKC_data_quality_heatmap.png" target="_blank">SKC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/SKC_weather_sensitivity_heatmap.png" target="_blank">SKC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/SKC_Breakout_Heatmap.png" target="_blank">SKC Breakout Heatmap</a></li></ul>
        </details>
    
* **UCIE:** Provides electricity data for **370 customers** in **Portugal** from **January 1, 2011, to January 1, 2015 (1,461 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/UCIE_data_quality_heatmap.png" target="_blank">UCIE Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/UCIE_weather_sensitivity_heatmap.png" target="_blank">UCIE Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/UCIE_Breakout_Heatmap.png" target="_blank">UCIE Breakout Heatmap</a></li></ul>
        </details>
    
* **ULE:** Data from **one building** in **Cambridge** recorded from **June 1, 2023, to May 31, 2024 (365 days)** at an **hourly resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/ULE_data_quality_heatmap.png" target="_blank">ULE Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/ULE_weather_sensitivity_heatmap.png" target="_blank">ULE Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/ULE_Breakout_Heatmap.png" target="_blank">ULE Breakout Heatmap</a></li></ul>
        </details>
    
* **UNICON:** Includes measurements across **64 buildings** in **Australia** from **January 1, 2018, to April 30, 2022 (1,580 days)** with **15-minute and 1-hour processed resolutions**. (CC BY-NC-SA 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/commercial/UNICON_data_quality_heatmap.png" target="_blank">UNICON Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/commercial/UNICON_weather_sensitivity_heatmap.png" target="_blank">UNICON Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/commercial/UNICON_Breakout_Heatmap.png" target="_blank">UNICON Breakout Heatmap</a></li></ul>
        </details>

### Residential Datasets:

* **AMPD:** Comprises **one Canadian household's** data from **April 1, 2012, to April 1, 2014 (730 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/AMPD_data_quality_heatmap.png" target="_blank">AMPD Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/AMPD_weather_sensitivity_heatmap.png" target="_blank">AMPD Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/AMPD_Breakout_Heatmap.png" target="_blank">AMPD Breakout Heatmap</a></li></ul>
        </details>
    
* **CEEW:** Electricity consumption from **84 smart meters** in **India** spanning **May 1, 2019, to October 31, 2021 (914 days)**. Processed at **3-minute, 15-minute, and 1-hour resolutions**. (CC0 1.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul>
            <li><a href="Visualization/Data_Quality_Heatmaps/residential/CEEW_Bareilly_data_quality_heatmap.png" target="_blank">Bareilly District</a></li>
            <li><a href="Visualization/Data_Quality_Heatmaps/residential/CEEW_Mathura_data_quality_heatmap.png" target="_blank">Mathura District</a></li>
        </ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul>
            <li><a href="Visualization/Weather_Correlation_Heatmaps/residential/CEEW_Bareilly_weather_sensitivity_heatmap.png" target="_blank">Bareilly District</a></li>
            <li><a href="Visualization/Weather_Correlation_Heatmaps/residential/CEEW_Mathura_weather_sensitivity_heatmap.png" target="_blank">Mathura District</a></li>
        </ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul>
            <li><a href="Visualization/Breakout_Heatmaps/residential/CEEW_Bareilly_Breakout_Heatmap.png" target="_blank">Bareilly District</a></li>
            <li><a href="Visualization/Breakout_Heatmaps/residential/CEEW_Mathura_Breakout_Heatmap.png" target="_blank">Mathura District</a></li>
        </ul>
        </details>
    
* **DCB:** Energy Station data for **one building** in **Japan** spanning over twenty years from **June 1, 2001, to October 31, 2022 (7,822 days)** at an **hourly resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/DCB_data_quality_heatmap.png" target="_blank">DCB Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/DCB_weather_sensitivity_heatmap.png" target="_blank">DCB Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/DCB_Breakout_Heatmap.png" target="_blank">DCB Breakout Heatmap</a></li></ul>
        </details>
    
* **DEDDIAG:** Domestic demand for **15 homes** in **Germany** from **August 10, 2016, to December 9, 2020 (1,582 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/DEDDIAG_data_quality_heatmap.png" target="_blank">DEDDIAG Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/DEDDIAG_weather_sensitivity_heatmap.png" target="_blank">DEDDIAG Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/DEDDIAG_Breakout_Heatmap.png" target="_blank">DEDDIAG Breakout Heatmap</a></li></ul>
        </details>
    
* **DESM:** Meteorological and load data from **3 houses** in **France** from **May 1, 2020, to May 1, 2021 (365 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY-NC-ND 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/DESM_data_quality_heatmap.png" target="_blank">DESM Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/DESM_weather_sensitivity_heatmap.png" target="_blank">DESM Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/DESM_Breakout_Heatmap.png" target="_blank">DESM Breakout Heatmap</a></li></ul>
        </details>
    
* **DTH:** Data for **1,000 anonymized households** in the **Slovak Republic** for **395 days (January 1, 2016, to January 30, 2017)** at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/DTH_data_quality_heatmap.png" target="_blank">DTH Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/DTH_weather_sensitivity_heatmap.png" target="_blank">DTH Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/DTH_Breakout_Heatmap.png" target="_blank">DTH Breakout Heatmap</a></li></ul>
        </details>
    
* **ECCG:** PV and consumption profiles for **51 buildings** in **Portugal** for **365 days (January 1, 2019, to January 1, 2020)**. Processed at **15-minute and 1-hour resolutions**. (CC BY-NC-ND 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/ECCG_data_quality_heatmap.png" target="_blank">ECCG Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/ECCG_weather_sensitivity_heatmap.png" target="_blank">ECCG Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/ECCG_Breakout_Heatmap.png" target="_blank">ECCG Breakout Heatmap</a></li></ul>
        </details>
    
* **ECWM:** Data from **one residential house** in **Mexico** spanning **November 5, 2022, to January 5, 2024 (426 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/ECWM_data_quality_heatmap.png" target="_blank">ECWM Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/ECWM_weather_sensitivity_heatmap.png" target="_blank">ECWM Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/ECWM_Breakout_Heatmap.png" target="_blank">ECWM Breakout Heatmap</a></li></ul>
        </details>
    
* **ENERTALK:** Data from **22 residential houses** in **South Korea** from **September 1, 2016, to May 1, 2017 (242 days)** at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/ENERTALK_data_quality_heatmap.png" target="_blank">ENERTALK Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/ENERTALK_weather_sensitivity_heatmap.png" target="_blank">ENERTALK Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/ENERTALK_Breakout_Heatmap.png" target="_blank">ENERTALK Breakout Heatmap</a></li></ul>
        </details>
    
* **flEECe:** Data for **6 houses** in **Virginia, USA**, spanning **July 6, 2017, to March 22, 2018 (259 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/flEECe_data_quality_heatmap.png" target="_blank">flEECe Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/flEECe_weather_sensitivity_heatmap.png" target="_blank">flEECe Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/flEECe_Breakout_Heatmap.png" target="_blank">flEECe Breakout Heatmap</a></li></ul>
        </details>
    
* **GoiEner:** Data from **25,559 buildings** in **Spain** spanning **November 2, 2014, to June 8, 2022 (2,775 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/GoiEner_data_quality_heatmap.png" target="_blank">GoiEner Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/GoiEner_weather_sensitivity_heatmap.png" target="_blank">GoiEner Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/GoiEner_Breakout_Heatmap.png" target="_blank">GoiEner Breakout Heatmap</a></li></ul>
        </details>
    
* **GREEND:** Power consumption from **7 households** in **Italy and Austria** from **December 6, 2013, to June 29, 2015 (570 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/GREEND_data_quality_heatmap.png" target="_blank">GREEND Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/GREEND_weather_sensitivity_heatmap.png" target="_blank">GREEND Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/GREEND_Breakout_Heatmap.png" target="_blank">GREEND Breakout Heatmap</a></li></ul>
        </details>
    
* **HES:** Data for **16 households** across **England** from **May 1, 2010, to July 30, 2011 (455 days)** at a **1-hour resolution**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/HES_data_quality_heatmap.png" target="_blank">HES Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/HES_weather_sensitivity_heatmap.png" target="_blank">HES Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/HES_Breakout_Heatmap.png" target="_blank">HES Breakout Heatmap</a></li></ul>
        </details>
    
* **Honda SMART Home:** Data from **one residential home** in **Davis, California**, for the year **2020 (January 1 to December 31; 365 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY-NC-ND 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/Honda SMART Home_data_quality_heatmap.png" target="_blank">Honda SMART Home Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/Honda SMART Home_weather_sensitivity_heatmap.png" target="_blank">Honda SMART Home Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/Honda SMART Home_Breakout_Heatmap.png" target="_blank">Honda SMART Home Breakout Heatmap</a></li></ul>
        </details>
    
* **HSG:** Data from **11 households** in **Germany** from **December 11, 2014, to May 1, 2019 (1,602 days)**. Processed at **1-minute, 15-minute, and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/HSG_data_quality_heatmap.png" target="_blank">HSG Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/HSG_weather_sensitivity_heatmap.png" target="_blank">HSG Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/HSG_Breakout_Heatmap.png" target="_blank">HSG Breakout Heatmap</a></li></ul>
        </details>
    
* **HUE:** Consumption records from **28 households** in **British Columbia, Canada**, spanning **June 1, 2012, to May 20, 2020 (2,910 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/HUE_data_quality_heatmap.png" target="_blank">HUE Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/HUE_weather_sensitivity_heatmap.png" target="_blank">HUE Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/HUE_Breakout_Heatmap.png" target="_blank">HUE Breakout Heatmap</a></li></ul>
        </details>
    
* **iFlex:** Data from **4,429 households** in **Norway** from **January 6, 2020, to March 26, 2021 (445 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/iFlex_data_quality_heatmap.png" target="_blank">iFlex Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/iFlex_weather_sensitivity_heatmap.png" target="_blank">iFlex Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/iFlex_Breakout_Heatmap.png" target="_blank">iFlex Breakout Heatmap</a></li></ul>
        </details>
    
* **IHEPC:** Measurements from **one house** near **Paris, France**, from **December 16, 2006, to November 26, 2010 (1,441 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/IHEPC_data_quality_heatmap.png" target="_blank">IHEPC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/IHEPC_weather_sensitivity_heatmap.png" target="_blank">IHEPC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/IHEPC_Breakout_Heatmap.png" target="_blank">IHEPC Breakout Heatmap</a></li></ul>
        </details>
    
* **IPC-Residential:** Data for **one building** in **China** from **January 1, 2016, to December 31, 2021 (2,191 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/IPC-Residential_data_quality_heatmap.png" target="_blank">IPC-Residential Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/IPC-Residential_weather_sensitivity_heatmap.png" target="_blank">IPC-Residential Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/IPC-Residential_Breakout_Heatmap.png" target="_blank">IPC-Residential Breakout Heatmap</a></li></ul>
        </details>
    
* **IRH:** Load profiles for an energy community of **15 households** in **Ireland** for **366 days (January 1, 2020, to January 1, 2021)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/IRH_data_quality_heatmap.png" target="_blank">IRH Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/IRH_weather_sensitivity_heatmap.png" target="_blank">IRH Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/IRH_Breakout_Heatmap.png" target="_blank">IRH Breakout Heatmap</a></li></ul>
        </details>
    
* **LCL:** Smart meter data for **5,561 households** in **London** from **November 23, 2011, to February 28, 2014 (828 days)**. Processed at **30-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/LCL_data_quality_heatmap.png" target="_blank">LCL Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/LCL_weather_sensitivity_heatmap.png" target="_blank">LCL Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/LCL_Breakout_Heatmap.png" target="_blank">LCL Breakout Heatmap</a></li></ul>
        </details>
    
* **LEC:** Measurements from **172 buildings** in **Portugal** spanning **May 5, 2022, to September 2, 2023 (485 days)** at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/LEC_data_quality_heatmap.png" target="_blank">LEC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/LEC_weather_sensitivity_heatmap.png" target="_blank">LEC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/LEC_Breakout_Heatmap.png" target="_blank">LEC Breakout Heatmap</a></li></ul>
        </details>
    
* **METER:** UK data from **311 participants** recorded between **February 17, 2016, and January 17, 2019 (1,065 days)**. Processed at **30-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/METER_data_quality_heatmap.png" target="_blank">METER Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/METER_weather_sensitivity_heatmap.png" target="_blank">METER Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/METER_Breakout_Heatmap.png" target="_blank">METER Breakout Heatmap</a></li></ul>
        </details>
    
* **MFRED:** Data from **26 apartments** in the **Northeastern USA** for **365 days (January 1, 2019, to January 1, 2020)**. Processed at **15-minute and 1-hour resolutions**. (CC0 1.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/MFRED_data_quality_heatmap.png" target="_blank">MFRED Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/MFRED_weather_sensitivity_heatmap.png" target="_blank">MFRED Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/MFRED_Breakout_Heatmap.png" target="_blank">MFRED Breakout Heatmap</a></li></ul>
        </details>
    
* **MIHEC:** A family residence in **South Africa** monitored over **1,013 days (March 1, 2019, to December 8, 2021)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/MIHEC_data_quality_heatmap.png" target="_blank">MIHEC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/MIHEC_weather_sensitivity_heatmap.png" target="_blank">MIHEC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/MIHEC_Breakout_Heatmap.png" target="_blank">MIHEC Breakout Heatmap</a></li></ul>
        </details>
    
* **NDB:** Data from **one UK household** in 2022 spanning **April 15 to November 30 (229 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/NDB_data_quality_heatmap.png" target="_blank">NDB Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/NDB_weather_sensitivity_heatmap.png" target="_blank">NDB Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/NDB_Breakout_Heatmap.png" target="_blank">NDB Breakout Heatmap</a></li></ul>
        </details>
    
* **NEEA:** Energy metering study data from **206 households** in **Portland** spanning **August 29, 2018, to December 31, 2020 (855 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/NEEA_data_quality_heatmap.png" target="_blank">NEEA Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/NEEA_weather_sensitivity_heatmap.png" target="_blank">NEEA Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/NEEA_Breakout_Heatmap.png" target="_blank">NEEA Breakout Heatmap</a></li></ul>
        </details>
    
* **NESEMP:** Monitoring project data for **215 households** in **Scotland** from **November 2, 2010, to October 22, 2012 (720 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/NESEMP_data_quality_heatmap.png" target="_blank">NESEMP Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/NESEMP_weather_sensitivity_heatmap.png" target="_blank">NESEMP Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/NESEMP_Breakout_Heatmap.png" target="_blank">NESEMP Breakout Heatmap</a></li></ul>
        </details>
    
* **NEST-Residential:** Open building data from **2 buildings** in **Switzerland** recorded from **July 1, 2019, to June 30, 2023 (1,460 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/NEST-Residential_data_quality_heatmap.png" target="_blank">NEST-Residential Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/NEST-Residential_weather_sensitivity_heatmap.png" target="_blank">NEST-Residential Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/NEST-Residential_Breakout_Heatmap.png" target="_blank">NEST-Residential Breakout Heatmap</a></li></ul>
        </details>
    
* **Norwegian:** Consumption data for **1,136 households** in **Norway** spanning **October 1, 2020, to March 31, 2022 (546 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/Norwegian_data_quality_heatmap.png" target="_blank">Norwegian Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/Norwegian_weather_sensitivity_heatmap.png" target="_blank">Norwegian Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/Norwegian_Breakout_Heatmap.png" target="_blank">Norwegian Breakout Heatmap</a></li></ul>
        </details>
    
* **PES:** Data from **10 private homes** in the **USA and Europe** spanning **June 3, 2011, to January 29, 2014 (971 days)** at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/PES_data_quality_heatmap.png" target="_blank">PES Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/PES_weather_sensitivity_heatmap.png" target="_blank">PES Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/PES_Breakout_Heatmap.png" target="_blank">PES Breakout Heatmap</a></li></ul>
        </details>
    
* **Plegma:** Data from **13 Greek households** spanning **July 11, 2022, to September 30, 2023 (446 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/Plegma_data_quality_heatmap.png" target="_blank">Plegma Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/Plegma_weather_sensitivity_heatmap.png" target="_blank">Plegma Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/Plegma_Breakout_Heatmap.png" target="_blank">Plegma Breakout Heatmap</a></li></ul>
        </details>
    
* **Prayas:** Data from **116 homes** in **India** from **January 1, 2018, to June 30, 2020 (911 days)** at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/Prayas_data_quality_heatmap.png" target="_blank">Prayas Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/Prayas_weather_sensitivity_heatmap.png" target="_blank">Prayas Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/Prayas_Breakout_Heatmap.png" target="_blank">Prayas Breakout Heatmap</a></li></ul>
        </details>
    
* **REED:** Monitoring data from **46 households** in **Costa Rica** for **384 days (January 12, 2018, to January 31, 2019)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/REED_data_quality_heatmap.png" target="_blank">REED Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/REED_weather_sensitivity_heatmap.png" target="_blank">REED Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/REED_Breakout_Heatmap.png" target="_blank">REED Breakout Heatmap</a></li></ul>
        </details>
    
* **REFIT:** Electrical measurements for **20 UK households** over **568 days (December 17, 2013, to July 8, 2015)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/REFIT_data_quality_heatmap.png" target="_blank">REFIT Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/REFIT_weather_sensitivity_heatmap.png" target="_blank">REFIT Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/REFIT_Breakout_Heatmap.png" target="_blank">REFIT Breakout Heatmap</a></li></ul>
        </details>
    
* **RHC:** Data for **one household** in **Canada** from **April 1, 2012, to April 1, 2014 (730 days)**. Processed at **1-minute, 15-minute, and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/RHC_data_quality_heatmap.png" target="_blank">RHC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/RHC_weather_sensitivity_heatmap.png" target="_blank">RHC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/RHC_Breakout_Heatmap.png" target="_blank">RHC Breakout Heatmap</a></li></ul>
        </details>
    
* **RSL:** High-resolution data for **2,903 households** in **Sri Lanka** spanning **October 1, 2023, to December 23, 2024 (449 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/RSL_data_quality_heatmap.png" target="_blank">RSL Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/RSL_weather_sensitivity_heatmap.png" target="_blank">RSL Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/RSL_Breakout_Heatmap.png" target="_blank">RSL Breakout Heatmap</a></li></ul>
        </details>
    
* **SAVE:** Data for **4,691 households** in the **UK** spanning **July 9, 2016, to December 30, 2018 (904 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/SAVE_data_quality_heatmap.png" target="_blank">SAVE Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/SAVE_weather_sensitivity_heatmap.png" target="_blank">SAVE Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/SAVE_Breakout_Heatmap.png" target="_blank">SAVE Breakout Heatmap</a></li></ul>
        </details>
    
* **SFAC:** Data for **one apartment** in **China** from **May 31, 2021, to June 1, 2022 (366 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/SFAC_data_quality_heatmap.png" target="_blank">SFAC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/SFAC_weather_sensitivity_heatmap.png" target="_blank">SFAC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/SFAC_Breakout_Heatmap.png" target="_blank">SFAC Breakout Heatmap</a></li></ul>
        </details>
    
* **SFHG:** Load profiles for **38 homes** in **Germany** for **730 days (January 1, 2019, to December 31, 2020)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/SFHG_data_quality_heatmap.png" target="_blank">SFHG Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/SFHG_weather_sensitivity_heatmap.png" target="_blank">SFHG Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/SFHG_Breakout_Heatmap.png" target="_blank">SFHG Breakout Heatmap</a></li></ul>
        </details>
    
* **SGSC:** Trial data for **13,735 households** in **Australia** spanning **October 6, 2011, to March 4, 2014 (880 days)** at **30-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/SGSC_data_quality_heatmap.png" target="_blank">SGSC Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/SGSC_weather_sensitivity_heatmap.png" target="_blank">SGSC Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/SGSC_Breakout_Heatmap.png" target="_blank">SGSC Breakout Heatmap</a></li></ul>
        </details>
    
* **SMART-Star:** Data from **114 apartments** in the **USA** from **August 14, 2014, to December 28, 2016 (867 days)**. Processed at **15-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/SMART-Star_data_quality_heatmap.png" target="_blank">SMART-Star Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/SMART-Star_weather_sensitivity_heatmap.png" target="_blank">SMART-Star Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/SMART-Star_Breakout_Heatmap.png" target="_blank">SMART-Star Breakout Heatmap</a></li></ul>
        </details>
    
* **SRSA:** Data for **one student residence** in **South Africa** from **April 9, 2016, to January 31, 2018 (662 days)** at a **1-hour resolution**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/SRSA_data_quality_heatmap.png" target="_blank">SRSA Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/SRSA_weather_sensitivity_heatmap.png" target="_blank">SRSA Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/SRSA_Breakout_Heatmap.png" target="_blank">SRSA Breakout Heatmap</a></li></ul>
        </details>
    
* **UKST:** Trial data for **14,319 households** in **Great Britain** spanning **January 8, 2008, to September 30, 2010 (996 days)**. Processed at **30-minute and 1-hour resolutions**.
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/UKST_data_quality_heatmap.png" target="_blank">UKST Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/UKST_weather_sensitivity_heatmap.png" target="_blank">UKST Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/UKST_Breakout_Heatmap.png" target="_blank">UKST Breakout Heatmap</a></li></ul>
        </details>
    
* **WED:** Meteorological and load data for **5 households** in **Mexico** spanning **May 19, 2022, to June 1, 2023 (378 days)**. Processed at **15-minute and 1-hour resolutions**. (CC BY 4.0)
    * **Visualizations:**
        <details>
        <summary><b>Data Quality</b></summary>
        <ul><li><a href="Visualization/Data_Quality_Heatmaps/residential/WED_data_quality_heatmap.png" target="_blank">WED Data Quality Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Weather Correlation</b></summary>
        <ul><li><a href="Visualization/Weather_Correlation_Heatmaps/residential/WED_weather_sensitivity_heatmap.png" target="_blank">WED Weather Sensitivity Heatmap</a></li></ul>
        </details>
        <details>
        <summary><b>Breakout</b></summary>
        <ul><li><a href="Visualization/Breakout_Heatmaps/residential/WED_Breakout_Heatmap.png" target="_blank">WED Breakout Heatmap</a></li></ul>
        </details>

To know more about dataset, please visit [HuggingFace Datasets](https://huggingface.co/datasets/ai-iot/EnergyBench).

## Benchmarking Leaderboard

Table 3: Comparison of the performance of traditional models (naive, auto-ARIMA, linear regression, lightgbm), and TSFMs using median NRMSE across different residential datasets. 
(Bold - Best, Italics - $2^{nd}$ Best)

|		Dataset	    | Naive  | Auto-ARIMA | Linear Regression | LightGBM | Moirai |Chronos| TimesFM |Time-MoE|
|---------------------------|--------|--------|--------|--------|--------|-------------------|----------------|--------|
| AMPD             | 76.08  | 61.61  | 66.23  | 64.33  | 56.77  | 59.73             | 82.84          | 52.41  |
| CEEW             | 100.74 | 78.27  | 129.24 | 132.07 | 188.76 | 92.14             | 60.06          | 96.20  |
| DCB              | 43.31  | 34.30  | 15.06  | 12.99  | 17.89  | 13.33             | 13.22          | 12.09  |
| DESM             | 55.77  | 46.54  | 60.41  | 58.03  | 84.73  | 42.67             | 38.94          | 42.41  |
| DTH              | 107.22 | 79.57  | 36.04  | 36.53  | 38.73  | 32.16             | 33.79          | 30.79  |
| ECCC             | 104.10 | 80.5   | 87.07  | 83.73  | 69.34  | 76.48             | 64.02          | 63.47  |
| ECWM             | 48.69  | 40.22  | 53.52  | 50.39  | 38.84  | 39.45             | 37.70          | 39.68  |
| ENERTALK        | 75.69  | 60.65  | 382.28 | NaN    | 71.23  | 56.76             | 51.17          | 115.49 |
| flEECe           | 85.84  | 56.58  | 67.37  | 64.13  | 53.09  | 55.76             | 63.58          | 50.63  |
| GoiEner          | 142.20 | 115.04 | 129.24 | 126.80 | 119.95 | 118.10            | 108.25         | 176.72 |
| HES              | 118.23 | 97.58  | 112.78 | 118.36 | 95.67  | 100.29            | 91.46          | 94.18  |
| Honda SMART Home | 33.01  | 23.24  | 15.33  | 14.96  | 13.99  | 12.82             | 13.66          | 12.59  |
| HUE              | 99.69  | 85.00  | 212.78 | 220.58 | 83.23  | 84.50             | 75.06          | 131.82 |
| iFlex            | 45.65  | 36.60  | 43.34  | 46.11  | 35.18  | 34.89             | 43.20          | 75.95  |
| IHEPC            | 100.48 | 78.59  | 77.68  | 77.59  | 73.07  | 76.88             | 68.90          | 66.16  |
| IPC-Residential  | 51.20  | 34.76  | 50.27  | 52.93  | 106.48 | 14.23             | 11.87          | 28.26  |
| IRH              | 112.69 | 96.80  | 110.27 | 105.67 | 93.52  | 101.57            | 88.57          | 87.10  |
| LEC              | 144.14 | 109.87 | 148.53 | 142.08 | 172.42 | 128.87            | 87.78          | 120.93 |
| MFRED            | 37.84  | 33.31  | 34.58  | 33.21  | 26.01  | 24.26             | 33.74          | 25.03  |
| MIHEC            | 154.21 | 144.78 | 226.99 | 199.14 | 148.75 | 164.6             | 138.33         | 158.10 |
| NEEA             | 102.05 | 77.34  | 82.78  | 80.50  | 76.05  | 74.96             | 68.00          | 80.42  |
| NESEMP          | 137.4  | 102.7  | 151.02 | 168.79 | 103.63 | 96.31             | 81.66          | 142.77 |
| Norwegian       | 61.67  | 49.13  | 60.66  | 59.18  | 47.36  | 48.58             | 49.33          | 44.00  |
| PES              | 6.04   | 6.08   | 103.85 | NaN    | 2.68   | 3.10              | 2.86           | 4.38   |
| Plegma           | 186.82 | 153.26 | 182.59 | 178.07 | 165.49 | 165.71            | 151.61         | 171.28 |
| Prayas           | 96.50  | 77.08  | 89.71  | 89.35  | 139.70 | 74.76             | 68.42          | 96.22  |
| RHC              | 76.08  | 61.61  | 66.23  | 64.33  | 56.57  | 59.73             | 82.84          | 52.41  |
| RSL              | 101.80 | 81.49  | 123.07 | 138.23 | 103.44 | 81.99             | 66.02          | 125.01 |
| SAVE             | 1.00   | 1.02   | 2.25   | 37.87  | 1.09   | 1.37              | 2.79           | 34.70  |
| SFHG             | 108.52 | 90.18  | 97.28  | 95.78  | 96.60  | 92.58             | 93.94          | 97.06  |
| SGSC             | 128.87 | 101.44 | 110.16 | 107.25 | 96.86  | 101.93            | 91.09          | 118.67 |
| SMART-Star       | 91.81  | 71.35  | 107.14 | 104.59 | 120.06 | 76.14             | 69.74          | 81.88  |
| SRSA             | 59.52  | 46.29  | 53.30  | 52.52  | 151.53 | 42.53             | 39.31          | 50.10  |
| UKST             | 110.54 | 89.41  | 102.61 | 129.40 | 89.55  | 84.44             | 84.25          | 103.60 |
| WED              | 104.37 | 84.66  | 102.69 | 64.13  | 101.84 | 85.36             | 9.90           | 73.19  |
| **Average**          | 88.85  | 71.05  | 99.84  | 91.20  | 84.00  | *69.11* | **61.94** | 91.96  |

## Directory structure
```
.
└── Benchmarking/
    ├── Arima             <- STLF using Auto-ARIMA
    ├── LightGBM          <- STLF using LightGBM
    ├── Linear-Regression <- STLF using Linear Regression
    ├── Naive             <- STLF using Naive model
    ├── TimesFM           <- Zero-shot using TimesFM
    ├── Moirai            <- Zero-shot using Moirai
    └── Chronos           <- Zero-shot using Chronos
└── Data-preprocessing/
    ├── HES               <- Data-preprocessing for HES
    ├── METER             <- Data-preprocessing for METER
    ├── NEEA              <- Data-preprocessing for NEEA
    ├── NESEMP            <- Data-preprocessing for NESEMP
    ├── SAVE              <- Data-preprocessing for SAVE
    └── UKST              <- Data-preprocessing for UKST
└── README.md
└── LICENSE
```



### Note: This repository is under development.
