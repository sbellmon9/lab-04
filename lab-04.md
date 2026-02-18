Lab 04 - Visualizing Spatial Data
================
Shatavia Bellmon
2/17/26

### Load packages and data

``` r
#install.packages("devtools")
#devtools::install_github("tidyverse/dsbox")
```

``` r
library(tidyverse)
library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

??dennys

??laquinta

View(laquinta)

The Denny’s dataset has 1643 rows and 6 columns. Each row represents an
individual Denny’s location. The variables are address, city, state,
zip, longitude, and latitude.

### Exercise 2

The La Quinta dataset has 909 rows and 6 columns. Each row represents
the different locations of the La Quinta hotels. The variables are
address, city, state, zip, longitude, and latitude.

### Exercise 3

There are La Quintas in Ecuador, Columbia, Dubai, Turkiye, Georgia,
Australia, China, Mexico, and Canada. According to the website given,
there are no Denny’s outside the U.S.

### Exercise 4

One way to deteermine international locations would be to look at the
state abbreviations of each location and see if it belongs to a U.S.
state or not.

### Exercise 5

``` r
dennys %>% 
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 × 6
    ## # ℹ 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

### Exercise 6

There are no dennys locations outide the U.S.

``` r
dennys %>%
  mutate(country = "United States")
```

    ## # A tibble: 1,643 × 7
    ##    address                        city    state zip   longitude latitude country
    ##    <chr>                          <chr>   <chr> <chr>     <dbl>    <dbl> <chr>  
    ##  1 2900 Denali                    Anchor… AK    99503    -150.      61.2 United…
    ##  2 3850 Debarr Road               Anchor… AK    99508    -150.      61.2 United…
    ##  3 1929 Airport Way               Fairba… AK    99701    -148.      64.8 United…
    ##  4 230 Connector Dr               Auburn  AL    36849     -85.5     32.6 United…
    ##  5 224 Daniel Payne Drive N       Birmin… AL    35207     -86.8     33.6 United…
    ##  6 900 16th St S, Commons on Gree Birmin… AL    35294     -86.8     33.5 United…
    ##  7 5931 Alabama Highway, #157     Cullman AL    35056     -86.9     34.2 United…
    ##  8 2190 Ross Clark Circle         Dothan  AL    36301     -85.4     31.2 United…
    ##  9 900 Tyson Rd                   Hope H… AL    36043     -86.4     32.2 United…
    ## 10 4874 University Drive          Huntsv… AL    35816     -86.7     34.7 United…
    ## # ℹ 1,633 more rows

…

…

…

…

### Excercise 7

There are La Quintas in Ecuador, Columbia, Dubai, Turkiye, Georgia,
Australia, China, Mexico, and Canada.

### Excercise 8

``` r
lq <- laquinta
```

``` r
lq <- lq %>%
  mutate(country = case_when(
    state %in% states$abbreviation ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    
    # Mexico cities
    city %in% c("Aguascalientes", "Ciudad Juarez", "Poza Rica", 
                "Puebla", "Reynosa", "San Jose Chiapa") ~ "Mexico",
    
    # Turkiye cities
    city %in% c("Bodrum", "Cesme", "Giresun", "Istanbul") ~ "Turkiye",
    
    # China cities
    city %in% c("Chengdu", "Qionghai", "Suzhou", "Taiyuan", 
                "Turpan", "Weifang", "Zunyi") ~ "China",
    
    # New Zealand cities
    city %in% c("Auckland", "Queenstown") ~ "New Zealand",
    
    # UAE cities
    city %in% c("Abu Dhabi", "Dubai") ~ "United Arab Emirates",
    
    # Individual City/Country matches
    city == "Medellin" ~ "Colombia",
    city == "Ecuador"  ~ "Ecuador",
    city == "Georgia"  ~ "Georgia"
  ))
```

### Excercise 9

``` r
lq <- lq %>%
  filter(country == "United States")
```

California has the most amount of dennys. Alaska, Montana, South Dakota,
and Vermont had the fewest amounts of Dennys. This makes sense as
California is the biggest state in the U.S., so more land equals more
oppurtunity to build a dennys. The other states with only 1 dennys have
many rural areas so it there is not a lot of business that can come from
these states.
