---
title: "CanALE - Walkability"
author: "Daniel Fuller"
date: "2026-09-11"
output:
  html_document:
    keep_md: true
---



# Can-ALE 

Read in the Can-ALE data converted to DA Level


``` r
canale <- read_csv("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/CanALE_2016.csv")
```

```
## Rows: 56589 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (8): dwl_d, z_dwl_d, ale_index, ale_class, transit, z_transit, ale_trani...
## dbl (5): dauid, int_d, poi, z_int_d, z_poi
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
glimpse(canale)
```

```
## Rows: 56,589
## Columns: 13
## $ dauid             <dbl> 10010165, 10010166, 10010167, 10010168, 10010169, 10…
## $ int_d             <dbl> 37.1, 40.0, 44.5, 59.2, 53.2, 51.9, 39.1, 51.2, 42.6…
## $ dwl_d             <chr> "700.90002", "748.40002", "869.20001", "1056", "991.…
## $ poi               <dbl> 50, 52, 54, 61, 58, 39, 32, 21, 27, 31, 53, 47, 16, …
## $ z_int_d           <dbl> -0.21425921, -0.16116789, -0.07878482, 0.19033323, 0…
## $ z_dwl_d           <chr> "-0.19163157", "-0.15383206", "-0.057701942", "0.090…
## $ z_poi             <dbl> -0.032791525, -0.014827580, 0.003136365, 0.066010177…
## $ ale_index         <chr> "-0.43868232", "-0.32982755", "-0.1333504", "0.34729…
## $ ale_class         <chr> "2", "2", "2", "3", "3", "2", "2", "2", "2", "3", "3…
## $ transit           <chr> "45", "46", "51", "60", "53", "43", "32", "39", "38"…
## $ z_transit         <chr> "-0.0545245", "-0.023959989", "0.12886257", "0.40394…
## $ ale_tranist       <chr> "-0.4932068", "-0.35378754", "-0.00448783", "0.75123…
## $ ale_transit_class <chr> "2", "2", "2", "2", "2", "2", "2", "2", "2", "2", "3…
```

``` r
canale$ale_index <- as.numeric(canale$ale_index)
```

```
## Warning: NAs introduced by coercion
```

``` r
canale$ale_class <- as.factor(canale$ale_class)

summary(canale$ale_index)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.     NAs 
## -2.1247 -1.8874 -0.4782  0.0119  0.6979 43.7841     500
```

``` r
ggplot(data = canale, aes(ale_index)) + 
        geom_histogram() + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 500 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Can_Ale_Data_Prep_files/figure-html/unnamed-chunk-1-1.png)<!-- -->


Select the variables we want from the 2016 census geography conversion file.


``` r
conv_file <- read_csv("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/PCCF Results/2016_92-151_XBB.csv")
```

```
## Rows: 489905 Columns: 48
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (24): PRname/PRnom, PRename/PRanom, PRfname/PRfnom, PReabbr/PRaabbrev, P...
## dbl (23): DBuid/IDidu, DBpop2016/IDpop2016, DBtdwell2016/IDtlog2016, DBurdwe...
## lgl  (1): DBir2016/IDri2016
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
glimpse(conv_file)
```

```
## Rows: 489,905
## Columns: 48
## $ `DBuid/IDidu`                  <dbl> 10020117004, 10020117003, 10020117008, …
## $ `DBpop2016/IDpop2016`          <dbl> 36, 35, 46, 30, 26, 78, 93, 0, 100, 0, …
## $ `DBtdwell2016/IDtlog2016`      <dbl> 13, 21, 28, 28, 44, 35, 39, 0, 46, 0, 1…
## $ `DBurdwell2016/IDrh2016`       <dbl> 10, 16, 21, 15, 17, 33, 37, 0, 41, 0, 1…
## $ `DBarea2016/IDsup2016`         <dbl> 0.6124, 3.8578, 0.3800, 7.7079, 3.9179,…
## $ `DBir2016/IDri2016`            <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALS…
## $ `DAuid/ADidu`                  <dbl> 10020117, 10020117, 10020117, 10010746,…
## $ `DArplamx/ADlamx`              <dbl> 8852175, 8852175, 8852175, 8927992, 892…
## $ `DArplamy/ADlamy`              <dbl> 1980863, 1980863, 1980863, 2040576, 204…
## $ `DArplat/Adlat`                <dbl> 46.93298, 46.93298, 46.93298, 47.00466,…
## $ `DArplong/ADlong`              <dbl> -55.36201, -55.36201, -55.36201, -54.10…
## $ `PRuid/PRidu`                  <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10,…
## $ `PRname/PRnom`                 <chr> "Newfoundland and Labrador / Terre-Neuv…
## $ `PRename/PRanom`               <chr> "Newfoundland and Labrador", "Newfoundl…
## $ `PRfname/PRfnom`               <chr> "Terre-Neuve-et-Labrador", "Terre-Neuve…
## $ `PReabbr/PRaabbrev`            <chr> "N.L.", "N.L.", "N.L.", "N.L.", "N.L.",…
## $ `PRfabbr/PRfabbrev`            <chr> "T.-N.-L.", "T.-N.-L.", "T.-N.-L.", "T.…
## $ `FEDuid/CEFidu`                <dbl> 10002, 10002, 10002, 10001, 10001, 1000…
## $ `FEDname/CEFnom`               <chr> "Bonavista--Burin--Trinity", "Bonavista…
## $ `ERuid/REidu`                  <dbl> 1020, 1020, 1020, 1010, 1010, 1020, 102…
## $ `ERname/REnom`                 <chr> "South Coast--Burin Peninsula / C\xf4te…
## $ `CDuid/DRidu`                  <dbl> 1002, 1002, 1002, 1001, 1001, 1002, 100…
## $ `CDname/DRnom`                 <chr> "Division No.  2", "Division No.  2", "…
## $ `CDtype/DRgenre`               <chr> "CDR", "CDR", "CDR", "CDR", "CDR", "CDR…
## $ `ADAuid/ADAidu`                <dbl> 10020001, 10020001, 10020001, 10010035,…
## $ ADAcode                        <chr> "0001", "0001", "0001", "0035", "0035",…
## $ `CSDuid/SDRidu`                <dbl> 1002006, 1002006, 1002006, 1001214, 100…
## $ `CSDname/SDRnom`               <chr> "Division No.  2, Subd. F", "Division N…
## $ `CSDtype/SDRgenre`             <chr> "SNO", "SNO", "SNO", "SNO", "SNO", "SNO…
## $ `SACtype/CSSgenre`             <dbl> 7, 7, 7, 7, 7, 5, 5, 7, 7, 7, 7, 7, 5, …
## $ `SACcode/CSScode`              <chr> "999", "999", "999", "999", "999", "997…
## $ `CCSuid/SRUidu`                <dbl> 1002001, 1002001, 1002001, 1001214, 100…
## $ `CCSname/SRUnom`               <chr> "Division No.  2, Subd. E", "Division N…
## $ `DPLuid/LDidu`                 <dbl> 100100, 100100, 100100, 100101, 100101,…
## $ `DPLname/LDnom`                <chr> "Little St. Lawrence", "Little St. Lawr…
## $ `DPLtype/LDgenre`              <chr> "DPL", "DPL", "DPL", "DPL", "DPL", "DPL…
## $ `CMAPuid/RMRPidu`              <dbl> 10999, 10999, 10999, 10999, 10999, 1099…
## $ `CMAuid/RMRidu`                <chr> "999", "999", "999", "999", "999", "997…
## $ `CMAname/RMRnom`               <chr> "No metropolitan influenced zone (N.L.)…
## $ `CMAtype/RMRgenre`             <chr> "J", "J", "J", "J", "J", "H", "H", "J",…
## $ `CTuid/SRidu`                  <chr> "9910.00", "9910.00", "9910.00", "9910.…
## $ `CTcode/SRcode`                <chr> "9910", "9910", "9910", "9910", "9910",…
## $ `CTname/SRnom`                 <chr> "9910.00", "9910.00", "9910.00", "9910.…
## $ `POPCTRRAPuid/CTRPOPRRPidu`    <dbl> 109910, 109910, 109910, 109910, 109910,…
## $ `POPCTRRAuid/CTRPOPRRidu`      <chr> "9910", "9910", "9910", "9910", "9910",…
## $ `POPCTRRAname/CTRPOPRRnom`     <chr> "Newfoundland and Labrador Rural Area /…
## $ `POPCTRRAtype/CTRPOPRRgenre`   <dbl> 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, …
## $ `POPCTRRAclass/CTRPOPRRclasse` <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
```

``` r
conv_file <- conv_file |> select('DAuid/ADidu', 'CTuid/SRidu', 'CMAuid/RMRidu', 'CTcode/SRcode', 'CTname/SRnom', 'DBuid/IDidu')
```


``` r
canale_da_conv <- left_join(canale, conv_file, c("dauid" = "DAuid/ADidu"))

canale_da_conv$`CTuid/SRidu` <- as.numeric(canale_da_conv$`CTuid/SRidu`)
```

## Select and write a new clean file


``` r
canale_data_CSDUL <- canale_da_conv

selection <- c(
  da16uid = "dauid",
  cmauid = "CMAuid/RMRidu",
  ctcode = "CTcode/SRcode",
  ctname = "CTname/SRnom",
  can_ale = "ale_index"
)

canale_data_CSDUL <- canale_data_CSDUL |> select(all_of(selection))

canale_data_CSDUL <- distinct(canale_data_CSDUL)

write_csv(canale_data_CSDUL, "/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/canale_data_CSDUL.csv")
```

## Descriptive Statistics


``` r
canale_data_CSDUL$can_ale <- as.numeric(canale_data_CSDUL$can_ale)

rm_covsum(data=canale_data_CSDUL, 
covs=c('can_ale'), all.stats = TRUE)
```

<table class="table table" style="color: black; margin-left: auto; margin-right: auto; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">  </th>
   <th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;"> n=56589 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">can ale</span> </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 0.0 (2.8) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Q1,Q3) </td>
   <td style="text-align:right;"> -0.5 (-1.9, 0.7) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Range (min, max) </td>
   <td style="text-align:right;"> (-2.1, 43.8) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Missing </td>
   <td style="text-align:right;"> 500 </td>
  </tr>
</tbody>
</table>

``` r
ggplot(canale_data_CSDUL) + 
      geom_histogram(aes(can_ale))
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 500 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Can_Ale_Data_Prep_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

## Mapping 


``` r
da_map <- read_sf("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/lda_000b16a_e/lda_000b16a_e.shp")

da_map$DAUID <- as.numeric(da_map$DAUID)

canale_map <- full_join(da_map, canale_data_CSDUL, c("DAUID" = "da16uid"))

ggplot() +
  geom_sf(data = canale_map, aes(fill = can_ale), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Can_Ale_Data_Prep_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

## Map for Saskatchewan only


``` r
sask_map <- canale_map |> filter(PRNAME == "Saskatchewan")

ggplot() +
  geom_sf(data = sask_map, aes(fill = can_ale), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Can_Ale_Data_Prep_files/figure-html/unnamed-chunk-7-1.png)<!-- -->
