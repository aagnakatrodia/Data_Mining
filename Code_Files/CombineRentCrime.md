Combine Rent and Crime Dataset
================

<p>
This is a file to combine the rent and the crime dataset together. <br>The Data source for the rent dataset for the city of LA can be found here: <https://usc.data.socrata.com/Los-Angeles/Rent-Price-LA-/4a97-v5tx> <br> The crime dataset can be found here: <https://data.lacity.org/A-Safe-City/Crime-Data-from-2010-to-Present/y8tr-7khq> <br> As described in the file to find tract numbers, the crime dataset is modified to add the tract numbers based on the latitudes and longitudes. Both, the crime and rent dataset for the city of LA are merged on the basis of the tract column.
</p>
``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(readr)
library(rmarkdown)

#Read the complete Crime Dataset (With Tract Numbers)
dfFullData <- read.csv("~/Desktop/GitAdd/Data_Mining/Files/FullCrimeDataWTract.csv")

#Change Column Name to make it similar to Rent Data
names(dfFullData)[17]<-"Tract"
names(dfFullData)[21]<-"Year"
dfFullData<-within(dfFullData, rm("No"))
dfFullData<-within(dfFullData, rm("Address"))
dfFullData<-within(dfFullData, rm("DateReported"))
dfFullData<-within(dfFullData, rm("MOCodes"))
dfFullData<-within(dfFullData, rm("StatusCode"))
dfFullData<-within(dfFullData, rm("StatusDescription"))
head(dfFullData)
```

    ##   AreaName CrimeCode              CrimeCodeDescription  DRNumber DateOccurred
    ## 1  Topanga       624          BATTERY - SIMPLE ASSAULT 102109886      4/13/10
    ## 2  Topanga       330             BURGLARY FROM VEHICLE 102111597      5/22/10
    ## 3  Topanga       624          BATTERY - SIMPLE ASSAULT 102110832       5/4/10
    ## 4  Topanga       310                          BURGLARY 102113988       7/8/10
    ## 5  Topanga       330             BURGLARY FROM VEHICLE 102110706       5/5/10
    ## 6  Topanga       647 THROWING OBJECT AT MOVING VEHICLE 102109850      4/18/10
    ##               Location PremiseCode     PremiseDescription ReportingDistrict
    ## 1 (34.2193, -118.6355)         501 SINGLE FAMILY DWELLING              2102
    ## 2   (34.221, -118.646)         101                 STREET              2102
    ## 3 (34.2193, -118.6304)         501 SINGLE FAMILY DWELLING              2111
    ## 4 (34.2196, -118.6376)         501 SINGLE FAMILY DWELLING              2102
    ## 5  (34.2197, -118.606)         108            PARKING LOT              2105
    ## 6  (34.2197, -118.606)         101                 STREET              2105
    ##   TimeOccurred  Tract VictimAge VictimDescent VictimSex Year
    ## 1         1800 113231        70             W         M 2010
    ## 2         2300 113231        17             H         M 2010
    ## 3         2015 113231        71             W         F 2010
    ## 4         1530 113231        40             W         F 2010
    ## 5         1420 113232        21             H         M 2010
    ## 6         2150 113232        20             W         M 2010

``` r
#Read Rent Dataset
rentLA <- read.csv("~/Desktop/GitAdd/Data_Mining/Files/Rent.csv")
names(rentLA)[4]<-"Tract"
head(rentLA)
```

    ##            Variable Year Amount  Tract  Neighborhood                   Location
    ## 1 Median Rent Price 2015   1115 920023 Santa Clarita (34.4214975, -118.4905135)
    ## 2 Median Rent Price 2015   1038 534404        Cudahy   (33.966232, -118.190553)
    ## 3 Median Rent Price 2015   1031 533601          Bell  (33.9803325, -118.194495)
    ## 4 Median Rent Price 2015   1362 405302   West Covina  (34.0767645, -117.946434)
    ## 5 Median Rent Price 2015    919 204200 Boyle Heights   (34.043615, -118.205084)
    ## 6 Median Rent Price 2015   2137 574100    Long Beach  (33.814659, -118.1216115)
    ##     Date
    ## 1 1/1/15
    ## 2 1/1/15
    ## 3 1/1/15
    ## 4 1/1/15
    ## 5 1/1/15
    ## 6 1/1/15

``` r
#Merge Rent & Crime data by Tract Number
mergedf <- merge(dfFullData, rentLA, by= c("Tract", "Year"))
head(mergedf)
```

    ##    Tract Year AreaName CrimeCode
    ## 1 101110 2010 Foothill       860
    ## 2 101110 2010 Foothill       310
    ## 3 101110 2010 Foothill       420
    ## 4 101110 2010 Foothill       230
    ## 5 101110 2010 Foothill       740
    ## 6 101110 2010 Foothill       310
    ##                                      CrimeCodeDescription  DRNumber
    ## 1                             BATTERY WITH SEXUAL CONTACT 101613303
    ## 2                                                BURGLARY 111604972
    ## 3         THEFT FROM MOTOR VEHICLE - PETTY ($950 & UNDER) 101609883
    ## 4          ASSAULT WITH DEADLY WEAPON, AGGRAVATED ASSAULT 101607273
    ## 5 VANDALISM - FELONY ($400 & OVER, ALL CHURCH VANDALISMS) 101613099
    ## 6                                                BURGLARY 101614939
    ##   DateOccurred           Location.x PremiseCode       PremiseDescription
    ## 1      6/24/10  (34.256, -118.2969)         501   SINGLE FAMILY DWELLING
    ## 2     12/19/10 (34.2612, -118.2868)         501   SINGLE FAMILY DWELLING
    ## 3      4/30/10  (34.2559, -118.285)         104                 DRIVEWAY
    ## 4      3/10/10 (34.2595, -118.2857)         122 VEHICLE, PASSENGER/TRUCK
    ## 5      6/28/10 (34.2612, -118.2877)         122 VEHICLE, PASSENGER/TRUCK
    ## 6      7/30/10   (34.256, -118.296)         501   SINGLE FAMILY DWELLING
    ##   ReportingDistrict TimeOccurred VictimAge VictimDescent VictimSex
    ## 1              1638         1230        44             H         F
    ## 2              1638          800        41             W         M
    ## 3              1639         1600        43             H         M
    ## 4              1638         1815        24             A         M
    ## 5              1638         1140        40             W         M
    ## 6              1638          715        42             W         M
    ##            Variable Amount Neighborhood                Location.y   Date
    ## 1 Median Rent Price   1044      Tujunga (34.2595555, -118.293602) 1/1/10
    ## 2 Median Rent Price   1044      Tujunga (34.2595555, -118.293602) 1/1/10
    ## 3 Median Rent Price   1044      Tujunga (34.2595555, -118.293602) 1/1/10
    ## 4 Median Rent Price   1044      Tujunga (34.2595555, -118.293602) 1/1/10
    ## 5 Median Rent Price   1044      Tujunga (34.2595555, -118.293602) 1/1/10
    ## 6 Median Rent Price   1044      Tujunga (34.2595555, -118.293602) 1/1/10

``` r
#Write Rent Data to .csv file
write.csv(mergedf, "~/Desktop/GitAdd/Data_Mining/Files/Outputs/CrimeRentData.csv")
```
