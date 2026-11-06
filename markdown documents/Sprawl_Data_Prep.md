---
title: "CSDUL Data Prep - Sprawl"
output:
  html_document:
    keep_md: true
---



# PCCF+ Data

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

# Urban Sprawl Data

Read in the urban sprawl data original developed at the Census Tract level


``` r
sprawl_og <- read_csv("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/Sprawl_ava_2026-01-20_10-50-35_annual/Sprawl_2016.csv")
```

```
## Rows: 5721 Columns: 6
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (6): CTUID, POLYID, sprawl, lower, median, upper
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
glimpse(sprawl_og)
```

```
## Rows: 5,721
## Columns: 6
## $ CTUID  <dbl> 2050002, 2050003, 5350422, 2050005, 2050006, 5370140, 5370140, …
## $ POLYID <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, …
## $ sprawl <dbl> -0.619500, -0.267700, 0.130000, 0.024470, 0.176200, -0.308200, …
## $ lower  <dbl> -0.69920, -0.34340, 0.05424, -0.05400, 0.10030, -0.38690, -0.34…
## $ median <dbl> -0.619300, -0.267100, 0.129700, 0.024860, 0.176000, -0.308000, …
## $ upper  <dbl> -0.54090, -0.19120, 0.20600, 0.10250, 0.25290, -0.23030, -0.189…
```

``` r
summary(sprawl_og$sprawl)
```

```
##       Min.    1st Qu.     Median       Mean    3rd Qu.       Max. 
## -1.6020000 -0.3493000  0.0678000 -0.0000008  0.3640000  3.2650000
```

``` r
ggplot(data = sprawl_og, aes(sprawl)) + 
        geom_histogram() + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

![](Sprawl_Data_Prep_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

## Sprawl CANUE

Read in the CANUE developed sprawl data converted to the postal code level


``` r
sprawl_pc <- read_csv("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/Sprawl_ava_2026-01-20_10-50-35_annual/nhspw_ava_16.csv")
```

```
## Rows: 863541 Columns: 6
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): postalcode16, province
## dbl (4): nhspw16_01, nhspw16_02, nhspw16_03, nhspw16_04
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
glimpse(sprawl_pc)
```

```
## Rows: 863,541
## Columns: 6
## $ postalcode16 <chr> "A0A0A1", "A0A0A2", "A0A0A3", "A0A0A4", "A0A0A5", "A0A0A6…
## $ province     <chr> "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL…
## $ nhspw16_01   <dbl> -9999.000, -9999.000, -9999.000, -9999.000, -9999.000, -9…
## $ nhspw16_02   <dbl> -9999.000, -9999.000, -9999.000, -9999.000, -9999.000, -9…
## $ nhspw16_03   <dbl> -9999.000, -9999.000, -9999.000, -9999.000, -9999.000, -9…
## $ nhspw16_04   <dbl> -9999.000, -9999.000, -9999.000, -9999.000, -9999.000, -9…
```

``` r
summary(sprawl_og$nhspw16_01)
```

```
## Warning: Unknown or uninitialised column: `nhspw16_01`.
```

```
## Length  Class   Mode 
##      0   NULL   NULL
```

``` r
ggplot(data = sprawl_pc, aes(nhspw16_01)) + 
        geom_histogram() + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

![](Sprawl_Data_Prep_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

``` r
miss_var_summary(sprawl_pc)
```

```
## # A tibble: 6 × 3
##   variable     n_miss pct_miss
##   <chr>         <int>    <num>
## 1 postalcode16      0        0
## 2 province          0        0
## 3 nhspw16_01        0        0
## 4 nhspw16_02        0        0
## 5 nhspw16_03        0        0
## 6 nhspw16_04        0        0
```

## Joining Sprawl PC to PCCF+


``` r
sprawl_join <- full_join(sprawl_pc, pccf_plus, c("postalcode16" = "PCODE"))

sprawl_join <- sprawl_join %>% replace_with_na(replace = list(nhspw16_01 = -9999.0000))

summary(sprawl_join$nhspw16_01)
```

```
##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max.      NAs 
## -1.60200 -0.32930  0.01841 -0.03886  0.27200  3.26500   205192
```

``` r
ggplot(data = sprawl_join, aes(nhspw16_01)) + 
        geom_histogram() + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 205192 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Sprawl_Data_Prep_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

We remove sprawl values of -9999.0000 because those are missing.

## Join OG Sprawl data with CANUE PC Sprawl data

Here the CT name variable is sort of a mess, not clear why they don't have a proper CT variable. So I went here [https://www12.statcan.gc.ca/census-recensement/alternative_alternatif.cfm?l=eng&dispext=zip&teng=2016_92-151_XBB_csv.zip&loc=http://www12.statcan.gc.ca/census-recensement/2016/geo/ref/gaf/files-fichiers/2016_92-151_XBB_csv.zip&k=%20%20%20%2023271](https://www12.statcan.gc.ca/census-recensement/alternative_alternatif.cfm?l=eng&dispext=zip&teng=2016_92-151_XBB_csv.zip&loc=http://www12.statcan.gc.ca/census-recensement/2016/geo/ref/gaf/files-fichiers/2016_92-151_XBB_csv.zip&k=%20%20%20%2023271) to get the proper conversion file from DAIUD to CT. 


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

Select the variables we want from the 2016 census geography conversion file.


``` r
sprawl_db_conv <- full_join(sprawl_join, conv_file, c("DB16uid" = "DBuid/IDidu"))

sprawl_db_conv$ctuid <- sprawl_db_conv$`CTuid/SRidu`
sprawl_db_conv$ctuid <- as.numeric(sprawl_db_conv$ctuid)
```

## Group by DA for joined data

Do a group by 2016 DA to be able to join the CANUE sprawl data to the original sprawl data as a check.


``` r
sprawl_join_da <- sprawl_db_conv |> 
                    group_by(DA16uid) |>
                      summarize(
                        nhspw16_01 = mean(nhspw16_01, na.rm = TRUE),
                        postalcode16 = first(postalcode16),
                        DB16uid = first(DB16uid),
                        CTname = first(CTname),
                        CMA = first(CMA),
                        ctuid = first(ctuid),
                        Tracted = first(Tracted),
                        Lat = median(Lat, na.rm = TRUE),
                        Long = median(Long, na.rm = TRUE),                        
                      )
```

## Join original sprawl data and CANUE sprawl data with correct identifiers

Also do some data clearning to remove rows with no CMA and rows with NA in the CANUE sprawl value.


``` r
sprawl_join_ct <- full_join(sprawl_og, sprawl_join_da, c("CTUID" = "ctuid"), suffix = c(".x", ".y"))

sprawl_join_ct <- sprawl_join_ct |> drop_na(nhspw16_01)

table(sprawl_join_ct$CMA)
```

```
## 
##  000    1  205  305  310  320  408  421  433  442  447  450  462  468  505  521 
##  230  320  585  226  242  157  279 1231  307  263  151  130 6319    1 1815  213 
##  522  528  529  531  532  535  537  539  541  543  550  555  559  562  563  565 
##  140    2  158    1  563 7417 1176  595  715  212  216  709  506  145    4    1 
##  568  575  580  590  595  602  705  725  805  810  825  830  835  850  860  915 
##  317  107  221  152  235 1187  369  407  108  167 1739  148 1644   95  115  245 
##  918  925  930  932  933  935  938  970  999 
##    2  149  158  264 3434  569  172  155    1
```

``` r
sprawl_join_ct <- sprawl_join_ct %>% replace_with_na(replace = list(CMA = "000"))
table(sprawl_join_ct$CMA)
```

```
## 
##    1  205  305  310  320  408  421  433  442  447  450  462  468  505  521  522 
##  320  585  226  242  157  279 1231  307  263  151  130 6319    1 1815  213  140 
##  528  529  531  532  535  537  539  541  543  550  555  559  562  563  565  568 
##    2  158    1  563 7417 1176  595  715  212  216  709  506  145    4    1  317 
##  575  580  590  595  602  705  725  805  810  825  830  835  850  860  915  918 
##  107  221  152  235 1187  369  407  108  167 1739  148 1644   95  115  245    2 
##  925  930  932  933  935  938  970  999 
##  149  158  264 3434  569  172  155    1
```

``` r
sprawl_join_ct <- sprawl_join_ct |> drop_na(CMA)
```

## Check correspondence

Check the correspondence between the CANUE sprawl data converted from postal code to the original sprawl data at the CT level.


``` r
ggplot(data = sprawl_join_ct) +
        geom_point(aes(x = sprawl, y = nhspw16_01))
```

```
## Warning: Removed 20 rows containing missing values or values outside the scale range
## (`geom_point()`).
```

![](Sprawl_Data_Prep_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot(data = sprawl_join_ct) +
        geom_histogram(aes(sprawl), alpha = 0.5, fill = "red") +
        geom_histogram(aes(nhspw16_01), alpha = 0.5, fill = "blue")
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 20 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

![](Sprawl_Data_Prep_files/figure-html/unnamed-chunk-9-2.png)<!-- -->

Overall looks very very close. That's good. 

## Select and write a new clean file


``` r
glimpse(sprawl_join_ct)
```

```
## Rows: 36,959
## Columns: 15
## $ CTUID        <dbl> 2050002, 2050002, 2050002, 2050002, 2050002, 2050002, 205…
## $ POLYID       <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, …
## $ sprawl       <dbl> -0.61950, -0.61950, -0.61950, -0.61950, -0.61950, -0.6195…
## $ lower        <dbl> -0.69920, -0.69920, -0.69920, -0.69920, -0.69920, -0.6992…
## $ median       <dbl> -0.61930, -0.61930, -0.61930, -0.61930, -0.61930, -0.6193…
## $ upper        <dbl> -0.5409, -0.5409, -0.5409, -0.5409, -0.5409, -0.5409, -0.…
## $ DA16uid      <dbl> 12090728, 12090729, 12090730, 12090731, 12090896, 1209089…
## $ nhspw16_01   <dbl> -0.6195000, -0.6195000, -0.6195000, -0.5770987, -0.619500…
## $ postalcode16 <chr> "B3P1M6", "B3P1A1", "B3P0G5", "B3P1A8", "B3R0A7", "B3R1G8…
## $ DB16uid      <dbl> 12090728001, 12090729007, 12090730001, 12090731005, 12090…
## $ CTname       <chr> "2", "2", "2", "2", "2", "2", "2", "2", "2", "3", "3", "3…
## $ CMA          <chr> "205", "205", "205", "205", "205", "205", "205", "205", "…
## $ Tracted      <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
## $ Lat          <dbl> 44.61281, 44.61849, 44.62282, 44.62915, 44.60980, 44.6038…
## $ Long         <dbl> -63.61376, -63.57755, -63.59836, -63.60609, -63.61374, -6…
```

``` r
sprawl_data_CSDUL <- sprawl_join_ct

selection <- c(
  ctuid = "CTUID",
  da16uid = "DA16uid",
  postalcode16 = "postalcode16",
  cmauid = "CMA",
  ctname = "CTname",
  sprawl_score = "nhspw16_01"
)

sprawl_data_CSDUL <- sprawl_data_CSDUL |> select(all_of(selection))

write_csv(sprawl_data_CSDUL, "/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/sprawl_data_CSDUL.csv")
```

## Descriptive Statistics


``` r
rm_covsum(data=sprawl_data_CSDUL, 
covs=c('sprawl_score'),all.stats = TRUE)
```

<table class="table table" style="color: black; margin-left: auto; margin-right: auto; color: black; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;position: sticky; top:0; background-color: #FFFFFF;">  </th>
   <th style="text-align:right;position: sticky; top:0; background-color: #FFFFFF;"> n=36959 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> <span style="font-weight: bold;">sprawl score</span> </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 0.1 (0.6) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Q1,Q3) </td>
   <td style="text-align:right;"> 0.1 (-0.2, 0.4) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Range (min, max) </td>
   <td style="text-align:right;"> (-1.6, 3.3) </td>
  </tr>
</tbody>
</table>

## Mapping 


``` r
ct_map <- get_census(dataset='CA16', regions=list(C = "01"),
                          vectors=c("v_CA21_1", "v_CA21_2"),
                          level='CT', use_cache = TRUE, geo_format = 'sf', quiet = TRUE)

ct_map$GeoUID <- as.numeric(ct_map$GeoUID)

sprawl_map <- full_join(ct_map, sprawl_data_CSDUL, c("GeoUID" = "ctuid"))

ggplot() +
  geom_sf(data = sprawl_map, aes(fill = sprawl_score)) +
  scale_fill_viridis_c() +
  theme_minimal()
```

![](Sprawl_Data_Prep_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

## Map for Saskatoon only


``` r
saskatoon_map <- sprawl_map |> filter(`Region Name` == "Saskatoon")

ggplot() +
  geom_sf(data = saskatoon_map, aes(fill = sprawl_score)) +
  scale_fill_viridis_c() +
  theme_minimal()
```

![](Sprawl_Data_Prep_files/figure-html/unnamed-chunk-13-1.png)<!-- -->


