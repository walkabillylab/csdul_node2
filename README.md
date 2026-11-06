# CSDUL NODE 2 

Canadian Social Determinants Urban Laboratory (CSDUL) - Node 2 Neighbourhood Opportunity data and documentation. The purpose of nodes is to develop and validate existing and new indicators to be included in CSDUL and the decomposition analysis. Node 2 is called Neighbourhood Opportunity and is generally focused on environmental and neighbourhood level data, which some of is already available in the [Canadian Urban Environmental Health Research Consortium](https://canue.ca/).

## Data Summaries 

Data summaries are available below. The first file is the data documentation and the second is the code for basic data wrangling and visualization. All of these files are also available in the `pdf documents` folder and the rendered md files are available in the `markdown documents` folder. 

- **Urban Sprawl Index** (`sprawl_data_CSDUL.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/sprawl_score)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Sprawl_Data_Prep.md)

- **Dwelling Repair Needs** (`dewlling_data_CSDUL.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/csdul_node2/blob/main/pdf%20documents/Dwellings_Data_Documentation_CANUE.pdf)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Dwellings_Data_Prep.md)

- **Air Quality (Carbon Monoxide and PM2.5)** (`air_data_CSDUL.csv`; variable: `co_monoxide`)
    * [Data Methods Documentation](https://github.com/walkabillylab/csdul_node2/blob/main/pdf%20documents/Air_Quality_Documentation_CANUE.pdf)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Air_Quality_Data_Prep.md)

- **Gentrification Index** (`gentri_data_CSDUL.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/csdul_node2/blob/main/pdf%20documents/Gentrification_Documentation_CANUE.pdf)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Gentrification_Data_Prep.md)

- **Food Environment Index (mRFEI)** (`food_data_CSDUL.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/sprawl_score)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Food_Data_Prep.md)

- **Normalized Difference Vegetation Index (NDVI)** (`green_data_CSDUL_NDVI.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/csdul_node2/blob/main/pdf%20documents/Greenness_Data_Documentation_CANUE.pdf)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Greenness_Data_Prep_NDVI.md)

- **Canadian Active Living Environments (Can-ALE)** (`canale_data_CSDUL.csv`)
    * [Data Methods Documentation](https://can-ale.ca/)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Can_Ale_Data_Prep.md)

- **Tree Canopy Cover** (`tree_data_CSDUL.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/csdul_node2/blob/main/pdf%20documents/Tree_Canopy_Documentation_CANUE.pdf)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Tree_Canopy_Data_Prep.md)

- **Flood Susceptibility Index** (`flood_risk_data_CSDUL.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/csdul_node2/blob/main/pdf%20documents/Flood_Risk_Documentation_CANUE.pdf)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Flood_Risk_Data_Prep.md)

- **Land Surface Temperature** (`land_temp_data_CSDUL.csv`)
    * [Data Methods Documentation](https://github.com/walkabillylab/csdul_node2/blob/main/pdf%20documents/Land_Surface_Temp_Documentation_CANUE.pdf)
    * [Data Wrangling and Descriptive Statistics](https://github.com/walkabillylab/csdul_node2/blob/main/markdown%20documents/Land_Temp_Data_Prep.md)

## Variable Description Table

Detailed table about the data. If you prefer a `.csv` version there is one [here](https://github.com/walkabillylab/csdul_node2/blob/main/Node%202%20Data%20Summary.csv).

| Data Set Name | Description | Key Indicator Variable | Variable Description | Units | Primary Geography | Methodological Documentation |
|---------------|-------------|----------------------|---------------------|-------|-------------------|-----------------------------|
| sprawl_data_CSDUL.csv | Urban Sprawl index for Census Tracts (within CMAs) for Canada in 2016. | sprawl_score | A summary measure of urban sprawl ranging theoretically between -3 and +3. This variable is a z-score of the combination of 9 different indicators. | Unitless. Theoretical range from -3 to +3. Standard normal distribution. Higher values mean less urban sprawl. | Census Tract | https://github.com/walkabillylab/sprawl_score |
| dewlling_data_CSDUL.csv | Number of dwellings in need of repair at the DA level based on the 25% sample of the census. | dwellings_repair | The proportion of dwellings in need of repair at the dissemination area level in Canada. | Proportion. Range 0 to 1. Higher values mean more dwellings in need of repair. | Dissemination Area | https://canuedata.ca/metadata.php |
| air_data_CSDUL.csv | Average annual air quality at the DA level between 2012 and 2014 for two metrics, PM2.5 and Carbon Monoxide. | co_monoxide | Annual Mean MOPITT CO (carbon monoxide) Surface Concentration (2012-2014) in ppb. | Parts per Billion. Range 109.5 to 289.1. Higher values mean more carbon monoxide. | Dissemination Area | https://canuedata.ca/metadata.php |
| air_data_CSDUL.csv | Average annual air quality at the DA level between 2012 and 2014 for two metrics, PM2.5 and Carbon Monoxide. | pm_2_5 | Annual Mean Satellite-derived PM2.5 (fine particulates) Surface Concentration (2012-2014) in ug/m3. | Micrograms per Cubic Meter. Range 0.72 to 13.3. Higher values mean more PM2.5. | Dissemination Area | https://canuedata.ca/metadata.php |
| gentri_data_CSDUL.csv | Gentrification measure developed by Steinmetz-Wood (https://doi.org/10.1186/s12942-017-0096-6). | gentrification | Gentrified census tract according to Steinmetz-Wood in 2016. | Binary. 1 = gentrified, 0 = otherwise. | Census Tract | https://canuedata.ca/metadata.php |
| food_data_CSDUL.csv | Modified Retail Food Environment Index (mRFEI) Canada 1 km (https://www150.statcan.gc.ca/n1/pub/13-20-0001/132000012022001-eng.htm). | food_environment | The modified Retail Food Environment Index (mRFEI) calculates the proportion of food outlets that sell a wide selection of fresh and nutritious food within each buffer. | Categorical. Range 0 to 4, with 4 being the healthiest food environment and 0 the least healthy. | Dissemination Area | https://canuedata.ca/metadata.php |
| green_data_CSDUL_NDVI.csv | Annual estimates of average normalized difference vegetation index (NDVI) and green/grey classification. Urban greenness assesses the condition and health of urban landscapes. Vegetation contributes to more livable communities by helping clean the air, moderate climate, control water flow, and provide wildlife habitat. | greeness | Annual average NDVI derived from AVHRR satellite imagery at 1 km resolution, producing cloud-free annual composites for Canada. | Range 0 to 1. Higher values mean more greenness. | Dissemination Area | https://canuedata.ca/metadata.php |
| canale_data_CSDUL.csv | The Canadian Active Living Environments (Can-ALE) database is a geographic-based set of measures representing the active-living friendliness of Canadian communities. | can_ale | Combined z-score based on intersection density, dwelling density, and points of interest. Transit stops are additionally incorporated within CMAs. | Combined z-score. Range -2.1 to +43.8. Higher values indicate more active-living-friendly environments. | Dissemination Area | https://can-ale.ca/ |
| tree_data_CSDUL.csv | Tree canopy is defined as vegetation (leaves, stems, branches, etc.) of woody plants greater than 5 m in height. Derived from the GFCC Surface Reflectance product. | tree_cover | Estimated percent of pixels covered by woody vegetation greater than 5 m in height. | Average percentage of pixels within a DA covered by trees. Range 0 to 78. Higher values indicate more tree cover. | Dissemination Area | https://canuedata.ca/metadata.php |
| Flood Susceptibility Index | Flood Susceptibility Index (FSI) dataset from Natural Resources Canada, based on historical flood events and ensemble machine learning methods. | flood_risk | Average flood risk over 3 years within a 500 m radius of the DA centroid. | Values close to 0 indicate low susceptibility and values close to 100 indicate high susceptibility. Range 2 to 98. | Dissemination Area | https://canuedata.ca/metadata.php |
| Land Surface Temperature | Annual estimates of maximum mean warm-season land surface temperature (LST) from Landsat 8 at 30 m resolution. | land_temp | Average land surface temperature over 3 years within a 500 m radius of the DA centroid. | Degrees Celsius. Range 3.3 to 37.5. | Dissemination Area | https://canuedata.ca/metadata.php |


