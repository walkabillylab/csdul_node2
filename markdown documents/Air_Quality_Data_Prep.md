---
title: "Air Quality"
author: "Daniel Fuller"
date: "2026-09-11"
output:
  html_document:
    keep_md: true
---



# Air Quality

Read in the CANUE developed air quality data converted to the postal code level


``` r
air_pc <- read_csv("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/Air Quality Index_ava_2026-01-19_14-07-47_annual_2014/aqaix_ava_14.csv")
```

```
## Rows: 856254 Columns: 12
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): postalcode14, province
## dbl (10): aqaix14_01, aqaix14_02, aqaix14_03, aqaix14_04, aqaix14_05, aqaix1...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
glimpse(air_pc)
```

```
## Rows: 856,254
## Columns: 12
## $ postalcode14 <chr> "A0A0A1", "A0A0A2", "A0A0A3", "A0A0A4", "A0A0A5", "A0A0A6…
## $ province     <chr> "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL…
## $ aqaix14_01   <dbl> -9999.00, 8.33, 9.37, 8.83, -9999.00, 8.83, 8.55, -9999.0…
## $ aqaix14_02   <dbl> -9999.00, 42.33, 40.32, 40.85, -9999.00, 40.85, 40.30, -9…
## $ aqaix14_03   <dbl> -9999.00, 37.38, 35.53, 36.67, -9999.00, 36.67, 36.12, -9…
## $ aqaix14_04   <dbl> -9999.00, 130.86, 131.78, 130.63, -9999.00, 130.63, 130.5…
## $ aqaix14_05   <dbl> -9.999000e+03, 2.893399e+15, 2.314333e+15, 2.295955e+15, …
## $ aqaix14_06   <dbl> -9999.00, 1.37, 1.34, 1.38, -9999.00, 1.38, 1.38, -9999.0…
## $ aqaix14_07   <dbl> -9999.00, 0.13, 0.15, 0.23, -9999.00, 0.23, 0.19, -9999.0…
## $ aqaix14_08   <dbl> -9999.00, 25.88, 26.37, 25.53, -9999.00, 25.53, 25.64, -9…
## $ aqaix14_09   <dbl> -9999.00, 2.98, 3.47, 3.40, -9999.00, 3.40, 3.15, -9999.0…
## $ aqaix14_10   <dbl> -9999.00, -0.11, 0.10, 0.02, -9999.00, 0.02, 0.08, -9999.…
```

``` r
summary(air_pc$aqaix14_04)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## -9999.0   149.9   180.4  -202.0   208.4   290.0
```

``` r
summary(air_pc$aqaix14_09)
```

```
##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
## -9999.00     5.18     6.83  -448.16     8.27    13.30
```

``` r
ggplot(data = air_pc, aes(aqaix14_04)) + 
        geom_histogram() + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

``` r
ggplot(data = air_pc, aes(aqaix14_09)) + 
        geom_histogram() + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-1-2.png)<!-- -->

## Joining Sprawl PC to PCCF+

Read in the PCCF+ data


``` r
pccf_plus <- read_csv("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/PCCF Results/sampledat_out.csv")
```

```
## Rows: 863541 Columns: 83
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (31): CODER, VERSION, PCODE, DB, DB_ir2021, CSDname, CSDtype, CMA, CMAty...
## dbl (51): PR, DAuid, CSDuid, Tracted, SACcode, SACtype, CCSuid, FEDuid, DPLu...
## lgl  (1): ID
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
glimpse(pccf_plus)
```

```
## Rows: 863,541
## Columns: 83
## $ CODER         <chr> "R", "R", "R", "R", "R", "R", "R", "R", "R", "R", "R", "…
## $ VERSION       <chr> "8B", "8B", "8B", "8B", "8B", "8B", "8B", "8B", "8B", "8…
## $ ID            <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ PCODE         <chr> "A0A0A1", "A0A0A2", "A0A0A3", "A0A0A4", "A0A0A5", "A0A0A…
## $ PR            <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, …
## $ DAuid         <dbl> 10010562, 10010520, 10010690, 10010549, 10010520, 100106…
## $ DB            <chr> "011", "007", "037", "005", "007", "037", "010", "036", …
## $ DB_ir2021     <chr> "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "…
## $ CSDuid        <dbl> 1001464, 1001374, 1001452, 1001434, 1001374, 1001452, 10…
## $ CSDname       <chr> "Avondale", "Division No.  1, Subd. I", "Division No.  1…
## $ CSDtype       <chr> "T", "SNO", "SNO", "T", "SNO", "SNO", "SNO", "SNO", "SNO…
## $ CMA           <chr> "000", "000", "000", "000", "000", "000", "000", "000", …
## $ CMAtype       <chr> "G", "I", "G", "H", "I", "G", "I", "G", "G", "J", "G", "…
## $ CMAname       <chr> "Strong metropolitan influenced zone (N.L.) / Zone d'inf…
## $ CTname        <chr> "0000.00", "0000.00", "0000.00", "0000.00", "0000.00", "…
## $ Tracted       <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
## $ SACcode       <dbl> 996, 998, 996, 997, 998, 996, 998, 996, 996, 999, 996, 9…
## $ SACtype       <dbl> 4, 6, 4, 5, 6, 4, 6, 4, 4, 7, 4, 7, 4, 5, 6, 6, 6, 4, 6,…
## $ CCSuid        <dbl> 1001472, 1001357, 1001472, 1001472, 1001357, 1001472, 10…
## $ FEDuid        <dbl> 10001, 10001, 10001, 10001, 10001, 10001, 10001, 10001, …
## $ FEDname       <chr> "Avalon", "Avalon", "Avalon", "Avalon", "Avalon", "Avalo…
## $ DPLuid        <dbl> 10, 100385, 10, 10, 100385, 10, 100385, 100252, 10, 10, …
## $ DPLtype       <chr> NA, "DPL", NA, NA, "DPL", NA, "DPL", "DPL", NA, NA, NA, …
## $ DPLname       <chr> NA, "Bristols Hope", NA, NA, "Bristols Hope", NA, "Brist…
## $ ERuid         <dbl> 1010, 1010, 1010, 1010, 1010, 1010, 1010, 1010, 1010, 10…
## $ ERname        <chr> "Avalon Peninsula", "Avalon Peninsula", "Avalon Peninsul…
## $ CARuid        <dbl> 1001, 1001, 1001, 1001, 1001, 1001, 1001, 1001, 1001, 10…
## $ CARname       <chr> "Census Agricultural Region 1", "Census Agricultural Reg…
## $ PopCtrRAPuid  <dbl> 109910, 100136, 109910, 109910, 100136, 109910, 100136, …
## $ PopCtrRAname  <chr> "Newfoundland and Labrador Rural Area / R\xe9gion rurale…
## $ PopCtrRAtype  <dbl> 5, 4, 5, 5, 4, 5, 4, 5, 5, 5, 5, 5, 5, 5, 4, 5, 5, 5, 4,…
## $ PopCtrRAclass <dbl> 1, 2, 1, 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 2,…
## $ CSize         <dbl> 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5,…
## $ CSizeMIZ      <dbl> 5, 7, 5, 6, 7, 5, 7, 5, 5, 7, 5, 7, 5, 6, 7, 7, 7, 5, 7,…
## $ HRuid         <dbl> 1021, 1021, 1021, 1021, 1021, 1021, 1021, 1021, 1021, 10…
## $ HRename       <chr> "Eastern Rural Zone", "Eastern Rural Zone", "Eastern Rur…
## $ HRfname       <chr> "Eastern Rural Zone", "Eastern Rural Zone", "Eastern Rur…
## $ AHRuid        <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, …
## $ AHRename      <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ AHRfname      <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ SLI           <dbl> 1, 9, 9, 1, 9, 9, 9, 9, 9, 1, 1, 1, 1, 1, 9, 9, 9, 9, 9,…
## $ Rep_Pt_type   <dbl> 3, 9, 9, 3, 9, 9, 3, 9, 9, 3, 3, 3, 3, 3, 9, 9, 9, 9, 9,…
## $ RPF           <dbl> 3, 6, 6, 3, 6, 6, 5, 6, 6, 3, 3, 3, 3, 3, 6, 6, 6, 6, 6,…
## $ PCtype        <dbl> 3, 9, 9, 3, 9, 9, 9, 9, 9, 3, 3, 3, 3, 3, 9, 9, 9, 9, 9,…
## $ DMT           <chr> "W", "9", "9", "W", "9", "9", "W", "9", "9", "W", "W", "…
## $ H_DMT         <chr> "W", NA, NA, "W", NA, NA, "W", NA, NA, "W", "W", "W", "W…
## $ DMTDIFF       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ PO            <dbl> 1, 2, 2, 1, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2,…
## $ QI            <chr> "NNN", "999", "999", "NNN", "999", "999", "999", "999", …
## $ Source        <dbl> 1, 9, 9, 1, 9, 9, 9, 9, 9, 1, 1, 1, 6, 1, 9, 9, 9, 9, 9,…
## $ Lat           <dbl> 47.39675, 47.71381, 47.35304, 47.52908, 47.71381, 47.353…
## $ Long          <dbl> -53.22259, -53.21024, -53.29517, -53.27264, -53.21024, -…
## $ Link_Source   <chr> "F", "5", "5", "F", "5", "5", "C", "5", "5", "F", "F", "…
## $ Link          <dbl> 9, 0, 0, 9, 0, 0, 7, 0, 0, 9, 9, 6, 9, 9, 0, 0, 0, 0, 0,…
## $ nCD           <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
## $ nCSD          <dbl> 1, 2, 2, 1, 2, 2, 1, 2, 2, 1, 1, 2, 1, 1, 2, 2, 2, 2, 2,…
## $ PREC          <chr> "5", "4", "4", "5", "4", "4", "5", "4", "4", "5", "5", "…
## $ Comm_Name     <chr> "AVONDALE", NA, NA, "SOUTH RIVER", NA, NA, NA, NA, NA, "…
## $ AirLift       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ InstFlag      <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ Resflag       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ InuitLands    <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
## $ BTIPPE        <dbl> 44735, 58153, 55655, 55928, 58153, 55655, 58153, 55655, …
## $ ATIPPE        <dbl> 39951, 49097, 49980, 49108, 49097, 49980, 49097, 49980, …
## $ QABTIPPE      <dbl> 2, 4, 4, 4, 4, 4, 4, 4, 4, 999, 3, 4, 4, 2, 4, 4, 4, 4, …
## $ QNBTIPPE      <dbl> 1, 2, 2, 2, 2, 2, 2, 2, 2, 999, 2, 2, 2, 1, 2, 2, 2, 2, …
## $ DABTIPPE      <dbl> 4, 8, 8, 8, 8, 8, 8, 8, 8, 999, 6, 7, 7, 3, 8, 8, 8, 8, …
## $ DNBTIPPE      <dbl> 2, 4, 4, 4, 4, 4, 4, 4, 4, 999, 3, 3, 3, 2, 4, 4, 4, 4, …
## $ QAATIPPE      <dbl> 2, 4, 5, 4, 4, 5, 4, 5, 5, 999, 3, 4, 4, 1, 4, 4, 4, 5, …
## $ QNATIPPE      <dbl> 1, 2, 2, 2, 2, 2, 2, 2, 2, 999, 1, 2, 2, 1, 2, 2, 2, 2, …
## $ DAATIPPE      <dbl> 4, 8, 9, 8, 8, 9, 8, 9, 9, 999, 6, 7, 8, 2, 8, 8, 8, 9, …
## $ DNATIPPE      <dbl> 2, 4, 4, 4, 4, 4, 4, 4, 4, 999, 2, 3, 4, 1, 4, 4, 4, 4, …
## $ IMPFLG        <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0,…
## $ DA11uid       <dbl> 10010562, 10010520, 10010690, 10010549, 10010520, 100106…
## $ DB11uid       <dbl> 1001056204, 1001052007, 1001069014, 1001054905, 10010520…
## $ DA06uid       <dbl> 10010562, 10010520, 10010690, 10010549, 10010520, 100106…
## $ DA01uid       <dbl> 10010112, 10010372, 10010117, 10010088, 10010372, 100101…
## $ EA96uid       <dbl> 10006006, 10001056, 10007086, 10001005, 10001056, 100070…
## $ EA91uid       <dbl> 10006006, 10001056, 10007086, 10001005, 10001056, 100070…
## $ EA86uid       <dbl> 10006018, 10001062, 10006004, 10001009, 10001062, 100060…
## $ EA81uid       <dbl> 10006018, 10001062, 10006003, 10001009, 10001062, 100060…
## $ DA16uid       <dbl> 10010562, 10010520, 10010690, 10010549, 10010520, 100106…
## $ DB16uid       <dbl> 10010562004, 10010520007, 10010690014, 10010549005, 1001…
```

``` r
pccf_plus <- pccf_plus |> select(PCODE, CTname, DAuid, CSDuid, CMA, Tracted, DA16uid, DB16uid, Lat, Long)
```


``` r
air_join <- full_join(air_pc, pccf_plus, c("postalcode14" = "PCODE"))

air_join <- air_join %>% replace_with_na(replace = list(aqaix14_04 = -9999.0000))
air_join <- air_join %>% replace_with_na(replace = list(aqaix14_04 = -9))

air_join <- air_join %>% replace_with_na(replace = list(aqaix14_09 = -9999.0000))
air_join <- air_join %>% replace_with_na(replace = list(aqaix14_09 = -9))

summary(air_join$aqaix14_04)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.     NAs 
##   109.5   150.5   184.1   184.4   212.2   290.0   41789
```

``` r
summary(air_join$aqaix14_09)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.     NAs 
##   0.730   5.450   7.030   6.908   8.330  13.300   48246
```

``` r
ggplot(data = air_join) + 
        geom_histogram(aes(aqaix14_04), alpha = 0.5, fill = "red") + 
        geom_histogram(aes(aqaix14_09), alpha = 0.5, fill = "blue") + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 41789 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 48246 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

We remove air values of -9999.0000 and -9 because those are missing.

## Group by DA for joined data

Do a group by 2016 DA to be able to join the CANUE sprawl data to the original sprawl data as a check.


``` r
glimpse(air_join)
```

```
## Rows: 865,558
## Columns: 21
## $ postalcode14 <chr> "A0A0A1", "A0A0A2", "A0A0A3", "A0A0A4", "A0A0A5", "A0A0A6…
## $ province     <chr> "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL…
## $ aqaix14_01   <dbl> -9999.00, 8.33, 9.37, 8.83, -9999.00, 8.83, 8.55, -9999.0…
## $ aqaix14_02   <dbl> -9999.00, 42.33, 40.32, 40.85, -9999.00, 40.85, 40.30, -9…
## $ aqaix14_03   <dbl> -9999.00, 37.38, 35.53, 36.67, -9999.00, 36.67, 36.12, -9…
## $ aqaix14_04   <dbl> NA, 130.86, 131.78, 130.63, NA, 130.63, 130.59, NA, NA, 1…
## $ aqaix14_05   <dbl> -9.999000e+03, 2.893399e+15, 2.314333e+15, 2.295955e+15, …
## $ aqaix14_06   <dbl> -9999.00, 1.37, 1.34, 1.38, -9999.00, 1.38, 1.38, -9999.0…
## $ aqaix14_07   <dbl> -9999.00, 0.13, 0.15, 0.23, -9999.00, 0.23, 0.19, -9999.0…
## $ aqaix14_08   <dbl> -9999.00, 25.88, 26.37, 25.53, -9999.00, 25.53, 25.64, -9…
## $ aqaix14_09   <dbl> NA, 2.98, 3.47, 3.40, NA, 3.40, 3.15, NA, NA, 3.32, 3.17,…
## $ aqaix14_10   <dbl> -9999.00, -0.11, 0.10, 0.02, -9999.00, 0.02, 0.08, -9999.…
## $ CTname       <chr> "0000.00", "0000.00", "0000.00", "0000.00", "0000.00", "0…
## $ DAuid        <dbl> 10010562, 10010520, 10010690, 10010549, 10010520, 1001069…
## $ CSDuid       <dbl> 1001464, 1001374, 1001452, 1001434, 1001374, 1001452, 100…
## $ CMA          <chr> "000", "000", "000", "000", "000", "000", "000", "000", "…
## $ Tracted      <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ DA16uid      <dbl> 10010562, 10010520, 10010690, 10010549, 10010520, 1001069…
## $ DB16uid      <dbl> 10010562004, 10010520007, 10010690014, 10010549005, 10010…
## $ Lat          <dbl> 47.39675, 47.71381, 47.35304, 47.52908, 47.71381, 47.3530…
## $ Long         <dbl> -53.22259, -53.21024, -53.29517, -53.27264, -53.21024, -5…
```

``` r
air_join_da <- air_join |> 
                    group_by(DA16uid) |>
                      summarize(
                        aqaix14_04 = mean(aqaix14_04, na.rm = TRUE),
                        aqaix14_09 = mean(aqaix14_09, na.rm = TRUE),
                        postalcode14 = first(postalcode14),
                        DB16uid = first(DB16uid),
                        CTname = first(CTname),
                        CMA = first(CMA),
                        Tracted = first(Tracted),
                        Lat = median(Lat, na.rm = TRUE),
                        Long = median(Long, na.rm = TRUE),                        
                      )
```

## Join OG Sprawl data with CANUE PC Sprawl data

Here the CT name variable is sort of a mess, not clear why they don't have a proper CT variable. So I went here [https://www12.statcan.gc.ca/census-recensement/alternative_alternatif.cfm?l=eng&dispext=zip&teng=2016_92-151_XBB_csv.zip&loc=http://www12.statcan.gc.ca/census-recensement/2016/geo/ref/gaf/files-fichiers/2016_92-151_XBB_csv.zip&k=%20%20%20%2023271](https://www12.statcan.gc.ca/census-recensement/alternative_alternatif.cfm?l=eng&dispext=zip&teng=2016_92-151_XBB_csv.zip&loc=http://www12.statcan.gc.ca/census-recensement/2016/geo/ref/gaf/files-fichiers/2016_92-151_XBB_csv.zip&k=%20%20%20%2023271) to get the proper conversion file from DAIUD to CT. 

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
air_da_conv <- left_join(air_join_da, conv_file, c("DA16uid" = "DAuid/ADidu"))

air_da_conv$`CTuid/SRidu` <- as.numeric(air_da_conv$`CTuid/SRidu`)
```

## Select and write a new clean file


``` r
air_data_CSDUL <- air_da_conv

selection <- c(
  da16uid = "DA16uid",
  postalcode14 = "postalcode14",
  cmauid = "CMAuid/RMRidu",
  ctcode = "CTcode/SRcode",
  ctname = "CTname/SRnom",
  co_monoxide = "aqaix14_04",
  pm_2_5 = "aqaix14_09"
)

air_data_CSDUL <- air_data_CSDUL |> select(all_of(selection))

air_data_CSDUL <- distinct(air_data_CSDUL)

write_csv(air_data_CSDUL, "/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/air_data_CSDUL.csv")
```

## Descriptive Statistics


``` r
rm_covsum(data=air_data_CSDUL, 
covs=c('co_monoxide', 'pm_2_5'),all.stats = TRUE)
```

<table class="table table" style="color: black; margin-left: auto; margin-right: auto; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">  </th>
   <th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;"> n=48796 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">co monoxide</span> </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 185.6 (38.3) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Q1,Q3) </td>
   <td style="text-align:right;"> 193.6 (150.1, 224.4) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Range (min, max) </td>
   <td style="text-align:right;"> (109.5, 289.1) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Missing </td>
   <td style="text-align:right;"> 1373 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">pm 2 5</span> </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 6.9 (1.9) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Q1,Q3) </td>
   <td style="text-align:right;"> 7.1 (5.4, 8.3) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Range (min, max) </td>
   <td style="text-align:right;"> (0.7, 13.3) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Missing </td>
   <td style="text-align:right;"> 1614 </td>
  </tr>
</tbody>
</table>

``` r
ggplot(air_data_CSDUL) + 
      geom_histogram(aes(co_monoxide))
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 1373 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

``` r
ggplot(air_data_CSDUL) + 
      geom_histogram(aes(pm_2_5))
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 1614 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-8-2.png)<!-- -->

## Mapping 


``` r
da_map <- read_sf("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/lda_000b16a_e/lda_000b16a_e.shp")

da_map$DAUID <- as.numeric(da_map$DAUID)

air_map <- full_join(da_map, air_data_CSDUL, c("DAUID" = "da16uid"))

ggplot() +
  geom_sf(data = air_map, aes(fill = co_monoxide), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot() +
  geom_sf(data = air_map, aes(fill = pm_2_5), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-9-2.png)<!-- -->

## Map for Saskatchewan only


``` r
sask_map <- air_map |> filter(PRNAME == "Saskatchewan")

ggplot() +
  geom_sf(data = sask_map, aes(fill = co_monoxide), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

``` r
ggplot() +
  geom_sf(data = sask_map, aes(fill = pm_2_5), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Air_Quality_Data_Prep_files/figure-html/unnamed-chunk-10-2.png)<!-- -->

