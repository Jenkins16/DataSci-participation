---
title: "s07 Exercises: Tibble Joins"
output: 
  html_document:
    keep_md: true
    theme: paper
---

## Requirements

You will need data from Joey Bernhardt's `singer` R package for this exercise. 

You can download the singer data from the `USF-Psych-DataSci/Classroom` repo:


```r
library(tidyverse)
```

```
## -- Attaching packages ------------------------------------------------------------------------------------------ tidyverse 1.3.0 --
```

```
## v ggplot2 3.2.1     v purrr   0.3.3
## v tibble  2.1.3     v dplyr   0.8.3
## v tidyr   1.0.2     v stringr 1.4.0
## v readr   1.3.1     v forcats 0.4.0
```

```
## -- Conflicts --------------------------------------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
songs <- read_csv("https://github.com/USF-Psych-DataSci/Classroom/raw/master/data/singer/songs.csv")
```

```
## Parsed with column specification:
## cols(
##   title = col_character(),
##   artist_name = col_character(),
##   year = col_double()
## )
```

```r
locations <- read_csv("https://github.com/USF-Psych-DataSci/Classroom/raw/master/data/singer/loc.csv")
```

```
## Parsed with column specification:
## cols(
##   artist_name = col_character(),
##   city = col_character(),
##   release = col_character(),
##   title = col_character()
## )
```

If you want, you could instead install the `singer` package itself. To do that,
you'll need to install `devtools`. Running this code in your console should do 
the trick:

```
install.packages("devtools")
devtools::install_github("JoeyBernhardt/singer")
```

Load required packages:

```
library(tidyverse)
library(singer)
knitr::opts_chunk$set(fig.width=4, fig.height=3, warning = FALSE, fig.align = "center")
```

<!-- The following chunk allows errors when knitting -->



## Exercise 1: `singer`

The package `singer` comes with two smallish data frames about songs. 
Let's take a look at them (after minor modifications by renaming and shuffling):


```r
(time <- as_tibble(songs) %>% 
   rename(song = title))
```

```
## # A tibble: 22 x 3
##    song                             artist_name      year
##    <chr>                            <chr>           <dbl>
##  1 Corduroy                         Pearl Jam        1994
##  2 Grievance                        Pearl Jam        2000
##  3 Stupidmop                        Pearl Jam        1994
##  4 Present Tense                    Pearl Jam        1996
##  5 MFC                              Pearl Jam        1998
##  6 Lukin                            Pearl Jam        1996
##  7 It's Lulu                        The Boo Radleys  1995
##  8 Sparrow                          The Boo Radleys  1992
##  9 Martin_ Doom! It's Seven O'Clock The Boo Radleys  1995
## 10 Leaves And Sand                  The Boo Radleys  1993
## # ... with 12 more rows
```


```r
(album <- as_tibble(locations) %>% 
   select(title, everything()) %>% 
   rename(album = release,
          song  = title))
```

```
## # A tibble: 14 x 4
##    song                          artist_name    city        album               
##    <chr>                         <chr>          <chr>       <chr>               
##  1 Grievance                     Pearl Jam      Seattle, WA Binaural            
##  2 Stupidmop                     Pearl Jam      Seattle, WA Vitalogy            
##  3 Present Tense                 Pearl Jam      Seattle, WA No Code             
##  4 MFC                           Pearl Jam      Seattle, WA Live On Two Legs    
##  5 Lukin                         Pearl Jam      Seattle, WA Seattle Washington ~
##  6 Stuck On Amber                The Boo Radle~ Liverpool,~ Wake Up!            
##  7 It's Lulu                     The Boo Radle~ Liverpool,~ Best Of             
##  8 Sparrow                       The Boo Radle~ Liverpool,~ Everything's Alrigh~
##  9 High as Monkeys               The Boo Radle~ Liverpool,~ Kingsize            
## 10 Butterfly McQueen             The Boo Radle~ Liverpool,~ Giant Steps         
## 11 My One and Only Love          Carly Simon    New York, ~ Moonlight Serenade  
## 12 It Was So Easy  (LP Version)  Carly Simon    New York, ~ No Secrets          
## 13 I've Got A Crush On You       Carly Simon    New York, ~ Clouds In My Coffee~
## 14 "Manha De Carnaval (Theme fr~ Carly Simon    New York, ~ Into White
```


1. We really care about the songs in `time`. But, for which of those songs do we 
   know its corresponding album?


```r
time %>% 
  inner_join(album, by = c("song", "artist_name"))
```

```
## # A tibble: 13 x 5
##    song                       artist_name    year city        album             
##    <chr>                      <chr>         <dbl> <chr>       <chr>             
##  1 Grievance                  Pearl Jam      2000 Seattle, WA Binaural          
##  2 Stupidmop                  Pearl Jam      1994 Seattle, WA Vitalogy          
##  3 Present Tense              Pearl Jam      1996 Seattle, WA No Code           
##  4 MFC                        Pearl Jam      1998 Seattle, WA Live On Two Legs  
##  5 Lukin                      Pearl Jam      1996 Seattle, WA Seattle Washingto~
##  6 It's Lulu                  The Boo Radl~  1995 Liverpool,~ Best Of           
##  7 Sparrow                    The Boo Radl~  1992 Liverpool,~ Everything's Alri~
##  8 High as Monkeys            The Boo Radl~  1998 Liverpool,~ Kingsize          
##  9 Butterfly McQueen          The Boo Radl~  1993 Liverpool,~ Giant Steps       
## 10 My One and Only Love       Carly Simon    2005 New York, ~ Moonlight Serenade
## 11 It Was So Easy  (LP Versi~ Carly Simon    1972 New York, ~ No Secrets        
## 12 I've Got A Crush On You    Carly Simon    1994 New York, ~ Clouds In My Coff~
## 13 "Manha De Carnaval (Theme~ Carly Simon    2007 New York, ~ Into White
```

2. Go ahead and add the corresponding albums to the `time` tibble, being sure to 
   preserve rows even if album info is not readily available.


```r
time %>% 
  left_join(select(album, -city), by = c("song", "artist_name"))
```

```
## # A tibble: 22 x 4
##    song                        artist_name     year album                       
##    <chr>                       <chr>          <dbl> <chr>                       
##  1 Corduroy                    Pearl Jam       1994 <NA>                        
##  2 Grievance                   Pearl Jam       2000 Binaural                    
##  3 Stupidmop                   Pearl Jam       1994 Vitalogy                    
##  4 Present Tense               Pearl Jam       1996 No Code                     
##  5 MFC                         Pearl Jam       1998 Live On Two Legs            
##  6 Lukin                       Pearl Jam       1996 Seattle Washington November~
##  7 It's Lulu                   The Boo Radle~  1995 Best Of                     
##  8 Sparrow                     The Boo Radle~  1992 Everything's Alright Forever
##  9 Martin_ Doom! It's Seven O~ The Boo Radle~  1995 <NA>                        
## 10 Leaves And Sand             The Boo Radle~  1993 <NA>                        
## # ... with 12 more rows
```

3. Which songs do we have "year", but not album info?


```r
time %>% 
  anti_join(album, by = "song")
```

```
## # A tibble: 9 x 3
##   song                             artist_name      year
##   <chr>                            <chr>           <dbl>
## 1 Corduroy                         Pearl Jam        1994
## 2 Martin_ Doom! It's Seven O'Clock The Boo Radleys  1995
## 3 Leaves And Sand                  The Boo Radleys  1993
## 4 Comb Your Hair                   The Boo Radleys  1998
## 5 Mine Again                       Mariah Carey     2005
## 6 Don't Forget About Us            Mariah Carey     2005
## 7 Babydoll                         Mariah Carey     1997
## 8 Don't Forget About Us            Mariah Carey     2005
## 9 Vision Of Love                   Mariah Carey     1990
```

4. Which artists are in `time`, but not in `album`?


```r
time %>% 
  anti_join(album, by = "artist_name")
```

```
## # A tibble: 5 x 3
##   song                  artist_name   year
##   <chr>                 <chr>        <dbl>
## 1 Mine Again            Mariah Carey  2005
## 2 Don't Forget About Us Mariah Carey  2005
## 3 Babydoll              Mariah Carey  1997
## 4 Don't Forget About Us Mariah Carey  2005
## 5 Vision Of Love        Mariah Carey  1990
```


5. You've come across these two tibbles, and just wish all the info was 
   available in one tibble. What would you do?


```r
time %>% 
  full_join(select(album, -artist_name), by = "song")
```

```
## # A tibble: 23 x 5
##    song                  artist_name     year city         album                
##    <chr>                 <chr>          <dbl> <chr>        <chr>                
##  1 Corduroy              Pearl Jam       1994 <NA>         <NA>                 
##  2 Grievance             Pearl Jam       2000 Seattle, WA  Binaural             
##  3 Stupidmop             Pearl Jam       1994 Seattle, WA  Vitalogy             
##  4 Present Tense         Pearl Jam       1996 Seattle, WA  No Code              
##  5 MFC                   Pearl Jam       1998 Seattle, WA  Live On Two Legs     
##  6 Lukin                 Pearl Jam       1996 Seattle, WA  Seattle Washington N~
##  7 It's Lulu             The Boo Radle~  1995 Liverpool, ~ Best Of              
##  8 Sparrow               The Boo Radle~  1992 Liverpool, ~ Everything's Alright~
##  9 Martin_ Doom! It's S~ The Boo Radle~  1995 <NA>         <NA>                 
## 10 Leaves And Sand       The Boo Radle~  1993 <NA>         <NA>                 
## # ... with 13 more rows
```


## Exercise 2: LOTR

Load in three tibbles of data on the Lord of the Rings:


```r
fell <- read_csv("https://raw.githubusercontent.com/jennybc/lotr-tidy/master/data/The_Fellowship_Of_The_Ring.csv")
```

```
## Parsed with column specification:
## cols(
##   Film = col_character(),
##   Race = col_character(),
##   Female = col_double(),
##   Male = col_double()
## )
```

```r
ttow <- read_csv("https://raw.githubusercontent.com/jennybc/lotr-tidy/master/data/The_Two_Towers.csv")
```

```
## Parsed with column specification:
## cols(
##   Film = col_character(),
##   Race = col_character(),
##   Female = col_double(),
##   Male = col_double()
## )
```

```r
retk <- read_csv("https://raw.githubusercontent.com/jennybc/lotr-tidy/master/data/The_Return_Of_The_King.csv")
```

```
## Parsed with column specification:
## cols(
##   Film = col_character(),
##   Race = col_character(),
##   Female = col_double(),
##   Male = col_double()
## )
```

1. Combine these into a single tibble.


```r
bind_rows(fell, ttow, retk)
```

```
## # A tibble: 9 x 4
##   Film                       Race   Female  Male
##   <chr>                      <chr>   <dbl> <dbl>
## 1 The Fellowship Of The Ring Elf      1229   971
## 2 The Fellowship Of The Ring Hobbit     14  3644
## 3 The Fellowship Of The Ring Man         0  1995
## 4 The Two Towers             Elf       331   513
## 5 The Two Towers             Hobbit      0  2463
## 6 The Two Towers             Man       401  3589
## 7 The Return Of The King     Elf       183   510
## 8 The Return Of The King     Hobbit      2  2673
## 9 The Return Of The King     Man       268  2459
```

2. Which races are present in "The Fellowship of the Ring" (`fell`), but not in 
   any of the other ones?


```r
fell %>% 
  anti_join(ttow, by = "Race") %>% 
  anti_join(retk, by = "Race")
```

```
## # A tibble: 0 x 4
## # ... with 4 variables: Film <chr>, Race <chr>, Female <dbl>, Male <dbl>
```


## Exercise 3: Set Operations

Let's use three set functions: `intersect`, `union` and `setdiff`. We'll work 
with two toy tibbles named `y` and `z`, similar to Data Wrangling Cheatsheet


```r
(y <-  tibble(x1 = LETTERS[1:3], x2 = 1:3))
```

```
## # A tibble: 3 x 2
##   x1       x2
##   <chr> <int>
## 1 A         1
## 2 B         2
## 3 C         3
```


```r
(z <- tibble(x1 = c("B", "C", "D"), x2 = 2:4))
```

```
## # A tibble: 3 x 2
##   x1       x2
##   <chr> <int>
## 1 B         2
## 2 C         3
## 3 D         4
```

1. Rows that appear in both `y` and `z`


```r
intersect(y, z)
```

```
## # A tibble: 2 x 2
##   x1       x2
##   <chr> <int>
## 1 B         2
## 2 C         3
```

2. You collected the data in `y` on Day 1, and `z` in Day 2. 
   Make a data set to reflect that.


```r
union_all(
  mutate(y, day = "Day 1"),
  mutate(z, day = "Day 2")
)
```

```
## # A tibble: 6 x 3
##   x1       x2 day  
##   <chr> <int> <chr>
## 1 A         1 Day 1
## 2 B         2 Day 1
## 3 C         3 Day 1
## 4 B         2 Day 2
## 5 C         3 Day 2
## 6 D         4 Day 2
```

3. The rows contained in `z` are bad! Remove those rows from `y`.


```r
setdiff(y, z)
```

```
## # A tibble: 1 x 2
##   x1       x2
##   <chr> <int>
## 1 A         1
```


```r
install.packages("nycflights13")
```

```
## Installing package into 'C:/Users/Khalia/Documents/R/win-library/3.6'
## (as 'lib' is unspecified)
```

```
## Error in contrib.url(repos, "source"): trying to use CRAN without setting a mirror
```

```r
library(nycflights13)
```


```r
flights %>%
full_join(airlines, by = "carrier") %>%
  full_join(select(weather, -year,-month, -day, -hour), by = c("origin", "time_hour")) %>%
  full_join(planes, by = "tailnum") %>%
  full_join(rename(airports, "origin" = "faa"), by= "origin") 
```

```
## # A tibble: 344,968 x 44
##    year.x month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##     <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1   2013     1     1      517            515         2      830            819
##  2   2013     1     1      533            529         4      850            830
##  3   2013     1     1      542            540         2      923            850
##  4   2013     1     1      544            545        -1     1004           1022
##  5   2013     1     1      554            600        -6      812            837
##  6   2013     1     1      554            558        -4      740            728
##  7   2013     1     1      555            600        -5      913            854
##  8   2013     1     1      557            600        -3      709            723
##  9   2013     1     1      557            600        -3      838            846
## 10   2013     1     1      558            600        -2      753            745
## # ... with 344,958 more rows, and 36 more variables: arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>,
## #   name.x <chr>, temp <dbl>, dewp <dbl>, humid <dbl>, wind_dir <dbl>,
## #   wind_speed <dbl>, wind_gust <dbl>, precip <dbl>, pressure <dbl>,
## #   visib <dbl>, year.y <int>, type <chr>, manufacturer <chr>, model <chr>,
## #   engines <int>, seats <int>, speed <int>, engine <chr>, name.y <chr>,
## #   lat <dbl>, lon <dbl>, alt <dbl>, tz <dbl>, dst <chr>, tzone <chr>
```
