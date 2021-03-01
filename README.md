# SURF'S UP

## Overview
Analyzing temperature data for the months of June and December in Oahu, in order to determine if a surf and ice cream shop business is sustainable in Hawaii year-round. 

### Purpose

The purpose of this project is to:

- Determine the Summary Statistics for June
- Determine the Summary Statistics for December

### Analysis

Data Source: [Hawaii SQLite Database](hawaii.sqlite)

Software used: Python 3.7.6, Pandas, Jupyter Notebooks, SQLAlchemy, Numpy

Analysis Code: 
- Summary Statistics for June & December [Summary Statistics Code](SurfsUp_Challenge.ipynb)

### Results
The summary temperature statistics are shown in the tables below:

|June | December|
|-----|--------|
|![June Summary Table](Images/june_summary.png) | ![December Summary Table](Images/dec_summary.png)|

<br />

- The mean temperature in Oahu during the month of June is 74.94 F and during the month of December is 71.04 F. There is roughly 3-4 degree Farenheit difference between the average temperatures of the two months.

- The maximum temperatures in the month of June and December are 85 F and 83 F respectively. The difference between the maximum temperatures in June and December is 2 degrees Farenheit. 

- The minimum temperatures in the month of June and December are 64F and 56 F respectively. The difference between the minimum temperatures of the two months is 8 degrees Farenheit. 

### Summary
[comment]: <> (There is a high-level summary of the results and there are two additional queries to perform to gather more weather data for June and December.)

From the above temperature analysis results, it is evident that Oahu temperatures are quite similar throughout the year. However, to determine if a surf and ice cream shop business is sustainable in Oahu, more weather data should considered in the analysis. For example, analyzing the precipitation, cloud cover, wind speeds/direction and tide heights data. 

##### Analyzing Precipitation 
The following query can be used to analyze average precipitation in June. (It can be refactored to also find average precipitation in December)

    June_prcp = session.query(Measurement.prcp).\
    filter(extract('month', Measurement.date) == 6).all()
    June_prcp_list = [p for p in June_prcp for p in p]
    June_prcp_df = pd.DataFrame(June_prcp)
    June_prcp_df.describe()

##### Analyzing Precipitation And Temperature by Location 
Analysis can also be done on precipitation and temperature by location. But first, we can join the two tables like so: 

    df = pd.DataFrame(session.query(Measurement, Station).filter(Measurement.id == Station.id).all())

Various queries can be run using GROUP BY and ORDER BY latitudes and longitudes to get summaries on temperature and precipitation data by location. 
