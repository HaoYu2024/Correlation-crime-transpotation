# Final Project: Crime & Transportation Density in NYC

## Data Sources:
- Bike: [NYC Bike Stats](https://www.nyc.gov/html/dot/html/bicyclists/bikestats.shtml) (2020, January; renamed as 2021 by mistake)
- Crime: [NYPD Complaint Data Historic](https://data.cityofnewyork.us/Public-Safety/NYPD-Complaint-Data-Historic/qgea-i56i?category=Public-Safety&view_name=NYPD-Complaint-Data-Historic)
- Real-Time Passenger (Bus): [Real-Time Passenger Information Sign Locations Map](https://data.cityofnewyork.us/Transportation/Real-Time-Passenger-Information-Sign-Locations-Map/2haw-rqv4)

## Data Processing Overview:

### Bike Data:
- `202001-citibike-tripdata.csv` renamed to `2021.csv`
- Cleaned data via MapReduce -> `clean_data.txt`
- Analyzed nearby bikes with Scala -> `bikesortbylatitude.csv`
- Combined with `crimesortbylatitude.csv` -> `bikecrimeratio.csv`

### Crime Data:
- `crime_data.csv` -> MapReduce -> `output1000line.csv`
- Profiling nearby crime -> `bikecrimesortbylatitude.csv` / `bussortbylatitude.csv`

### Bus Data:
- `Real_Time_Passenger_Information_Sign_Locations.csv` renamed to `bus`
- Cleaned by MapReduce -> `bussortbylatitude`
- Analyzed by Scala -> `buscrimeratio.csv`

### Trendline:
- `bikecrimeratio.csv` / `buscrimeratio.csv` analyzed for trendline
- Visualized via CSV

## Project Introduction:
Our project aims to study the correlation between bike/bus density and the crime amount nearby. We define the density of bus/bike stations as the number of other bus/bike stations nearby each bus/bike station. To achieve this, we first use MapReduce to clean our source data, keeping only the latitude and longitude. Then, we use Scala to find the density of each coordinate. We define the range of nearby stations as those within a circle with a radius of 0.025. Finally, we use Scala to find the trendline and visualize it with CSV.

## Steps to Re-run the Project:
1. Download the source files from the websites above, or find them already downloaded in the `data_ingest/source_data` directory.
2. Clean the source files via MapReduce. The crime CSV should be shrunk down to the first 1000 lines only. (Check the `etl` directory for details.)
3. Use MapReduce to profile the data by counting the length of files before and after cleaning. (Check the `profile_code` directory.) After running MapReduce, use the replace function of the text editor to remove any extra zeros at the end if necessary.
4. Use Scala for the first analysis to get `bike/bus_sortbylatitude.csv` (Check the `ana_code/firstana` directory.)
5. Use Scala for the second analysis to get `bike/bus_crimeratio.csv` (Check the `ana_code/secondana` directory.) Be aware that headers need to be ignored in Scala or deleted from source files.
6. Use Scala for the third analysis to get the trendline for bus/bike density as the x-axis and crime amounts as the y-axis. (Check the `ana_code/secondana` directory.)
