---
title: "Greenness"
author: "Daniel Fuller"
date: "2026-09-11"
output:
  html_document:
    keep_md: true
---



# Greenness

Read in the CANUE developed greenness data converted to the postal code level


``` r
green_pc <- read_csv("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/AVHHR NDVI_2024-04-17_04-08-36_annual/gravh_amn_13.csv")
```

```
## Rows: 852193 Columns: 5
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): postalcode13, province
## dbl (3): gravh13_01, gravh13_02, gravh13_03
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
glimpse(green_pc)
```

```
## Rows: 852,193
## Columns: 5
## $ postalcode13 <chr> "A0A0A1", "A0A0A2", "A0A0A3", "A0A0A4", "A0A0A5", "A0A0A6…
## $ province     <chr> "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL…
## $ gravh13_01   <dbl> 0.71, 0.71, 0.65, 0.70, 0.57, 0.67, 0.70, 0.68, 0.22, 0.7…
## $ gravh13_02   <dbl> 0.26, 0.31, -0.51, 0.33, -0.05, 0.29, 0.11, 0.14, -0.30, …
## $ gravh13_03   <dbl> 0.30, 0.52, -0.73, 0.55, 0.51, 0.46, 0.65, 0.57, -9999.00…
```

``` r
summary(green_pc$gravh13_02)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## -0.8400  0.3200  0.3900  0.3928  0.4700  0.8000
```

``` r
ggplot(data = green_pc, aes(gravh13_02)) + 
        geom_histogram() + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

![](Greenness_Data_Prep_NDVI_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

## Joining PC to PCCF+

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
pccf_plus <- pccf_plus |> select(PCODE, CTname, DAuid, CSDuid, CMA, Tracted, DA16uid, DB16uid, Lat, Long)
```


``` r
green_join <- full_join(green_pc, pccf_plus, c("postalcode13" = "PCODE"))

green_join <- green_join %>% replace_with_na(replace = list(gravh13_02 = -9999.0000))
green_join <- green_join %>% replace_with_na(replace = list(gravh13_02 = -9))

summary(green_join$gravh13_02)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.     NAs 
## -0.8400  0.3200  0.3900  0.3928  0.4700  0.8000   14877
```

``` r
ggplot(data = green_join) + 
        geom_histogram(aes(gravh13_02), alpha = 0.5, fill = "red") + 
        theme_minimal()
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 14877 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Greenness_Data_Prep_NDVI_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

We remove air values of -9999.0000 and -9 because those are missing.

## Group by DA for joined data

Do a group by 2016 DA to be able to join the CANUE sprawl data to the original sprawl data as a check.


``` r
glimpse(green_join)
```

```
## Rows: 867,070
## Columns: 14
## $ postalcode13 <chr> "A0A0A1", "A0A0A2", "A0A0A3", "A0A0A4", "A0A0A5", "A0A0A6…
## $ province     <chr> "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL", "NL…
## $ gravh13_01   <dbl> 0.71, 0.71, 0.65, 0.70, 0.57, 0.67, 0.70, 0.68, 0.22, 0.7…
## $ gravh13_02   <dbl> 0.26, 0.31, -0.51, 0.33, -0.05, 0.29, 0.11, 0.14, -0.30, …
## $ gravh13_03   <dbl> 0.30, 0.52, -0.73, 0.55, 0.51, 0.46, 0.65, 0.57, -9999.00…
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
green_join_da <- green_join |> 
                    group_by(DA16uid) |>
                      summarize(
                        gravh13_02 = mean(gravh13_02, na.rm = TRUE),
                        postalcode13 = first(postalcode13),
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
conv_file <- conv_file |> select('DAuid/ADidu', 'CTuid/SRidu', 'CMAuid/RMRidu', 'CTcode/SRcode', 'CTname/SRnom', 'DBuid/IDidu')
```


``` r
green_da_conv <- left_join(green_join_da, conv_file, c("DA16uid" = "DAuid/ADidu"))

green_da_conv$`CTuid/SRidu` <- as.numeric(green_da_conv$`CTuid/SRidu`)
```

## Select and write a new clean file


``` r
green_data_CSDUL_NDVI <- green_da_conv

selection <- c(
  da16uid = "DA16uid",
  postalcode13 = "postalcode13",
  cmauid = "CMAuid/RMRidu",
  ctcode = "CTcode/SRcode",
  ctname = "CTname/SRnom",
  greenness = "gravh13_02"
)

green_data_CSDUL_NDVI <- green_data_CSDUL_NDVI |> select(all_of(selection))

green_data_CSDUL_NDVI <- distinct(green_data_CSDUL_NDVI)

write_csv(green_data_CSDUL_NDVI, "/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/green_data_CSDUL_NDVI.csv")
```

## Descriptive Statistics


``` r
rm_covsum(data=green_data_CSDUL_NDVI, 
covs=c('greenness'),all.stats = TRUE)
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
   <td style="text-align:left;"> <span style="font-weight: bold;">greenness</span> </td>
   <td style="text-align:right;">  </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Mean (sd) </td>
   <td style="text-align:right;"> 0.4 (0.1) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Median (Q1,Q3) </td>
   <td style="text-align:right;"> 0.4 (0.3, 0.5) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Range (min, max) </td>
   <td style="text-align:right;"> (-0.8, 0.8) </td>
  </tr>
  <tr>
   <td style="text-align:left;padding-left: 2em;" indentlevel="1"> Missing </td>
   <td style="text-align:right;"> 240 </td>
  </tr>
</tbody>
</table>

``` r
ggplot(green_data_CSDUL_NDVI) + 
      geom_histogram(aes(greenness))
```

```
## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.
```

```
## Warning: Removed 240 rows containing non-finite outside the scale range
## (`stat_bin()`).
```

![](Greenness_Data_Prep_NDVI_files/figure-html/unnamed-chunk-8-1.png)<!-- -->


## Mapping 


``` r
da_map <- read_sf("/Users/dlf545/Library/CloudStorage/OneDrive-UniversityofSaskatchewan/CSDUL data/CSDUL Data Transfer/lda_000b16a_e/lda_000b16a_e.shp")

da_map$DAUID <- as.numeric(da_map$DAUID)

green_map <- full_join(da_map, green_data_CSDUL_NDVI, c("DAUID" = "da16uid"))

ggplot() +
  geom_sf(data = green_map, aes(fill = greenness), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Greenness_Data_Prep_NDVI_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

## Map for Saskatchewan only


``` r
sask_map <- green_map |> filter(PRNAME == "Saskatchewan")

ggplot() +
  geom_sf(data = sask_map, aes(fill = greenness), color = NA) +
  scale_fill_viridis_c() +
  theme_void()
```

![](Greenness_Data_Prep_NDVI_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

