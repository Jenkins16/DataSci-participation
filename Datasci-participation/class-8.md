---
title: "Class 8"
output: 
  html_document:
    keep_md: true
    theme: paper
---


```r
# install.packages("here")
# install.packages("readxl")
# install.packages("haven")
# install.packages("ggthemes")
# install.packages("svglite")
# install.packages("rio")
```


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
library(gapminder)
library(here)
```

```
## Warning: package 'here' was built under R version 3.6.3
```

```
## here() starts at C:/Users/Khalia/Documents/GitHub/DataSci-participation/Datasci-participation
```

```r
library(readxl) 
library(haven)
library(dplyr)
library(ggthemes)
```

```
## Warning: package 'ggthemes' was built under R version 3.6.3
```

```r
library(svglite)
```

```
## Warning: package 'svglite' was built under R version 3.6.3
```

```r
library(rio)
```

```
## Warning: package 'rio' was built under R version 3.6.3
```




```
## # A tibble: 33 x 6
##    country          continent  year lifeExp        pop gdpPercap
##    <fct>            <fct>     <int>   <dbl>      <int>     <dbl>
##  1 Afghanistan      Asia       2007    43.8   31889923      975.
##  2 Bahrain          Asia       2007    75.6     708573    29796.
##  3 Bangladesh       Asia       2007    64.1  150448339     1391.
##  4 Cambodia         Asia       2007    59.7   14131858     1714.
##  5 China            Asia       2007    73.0 1318683096     4959.
##  6 Hong Kong, China Asia       2007    82.2    6980412    39725.
##  7 India            Asia       2007    64.7 1110396331     2452.
##  8 Indonesia        Asia       2007    70.6  223547000     3541.
##  9 Iran             Asia       2007    71.0   69453570    11606.
## 10 Iraq             Asia       2007    59.5   27499638     4471.
## # ... with 23 more rows
```






```
## Parsed with column specification:
## cols(
##   country = col_character(),
##   continent = col_character(),
##   year = col_double(),
##   lifeExp = col_double(),
##   pop = col_double(),
##   gdpPercap = col_double()
## )
```

```
## # A tibble: 33 x 6
##    country          continent  year lifeExp        pop gdpPercap
##    <chr>            <chr>     <dbl>   <dbl>      <dbl>     <dbl>
##  1 Afghanistan      Asia       2007    43.8   31889923      975.
##  2 Bahrain          Asia       2007    75.6     708573    29796.
##  3 Bangladesh       Asia       2007    64.1  150448339     1391.
##  4 Cambodia         Asia       2007    59.7   14131858     1714.
##  5 China            Asia       2007    73.0 1318683096     4959.
##  6 Hong Kong, China Asia       2007    82.2    6980412    39725.
##  7 India            Asia       2007    64.7 1110396331     2452.
##  8 Indonesia        Asia       2007    70.6  223547000     3541.
##  9 Iran             Asia       2007    71.0   69453570    11606.
## 10 Iraq             Asia       2007    59.5   27499638     4471.
## # ... with 23 more rows
```

```r
url <- "http://gattonweb.uky.edu/sheather/book/docs/datasets/magazines.csv"
```


```r
read_csv(url)
```

```
## Parsed with column specification:
## cols(
##   Magazine = col_character(),
##   AdRevenue = col_double(),
##   AdPages = col_double(),
##   SubRevenue = col_double(),
##   NewsRevenue = col_double()
## )
```

```
## # A tibble: 204 x 5
##    Magazine                             AdRevenue AdPages SubRevenue NewsRevenue
##    <chr>                                    <dbl>   <dbl>      <dbl>       <dbl>
##  1 Weekly World News                         2280    300         854       16568
##  2 National Examiner                         3382    380         968       27215
##  3 J-14                                      4218    250        2206       12453
##  4 Soap Opera Weekly                         4622    439        5555       24282
##  5 Easyriders                                5121    524.       4155        9929
##  6 Mary Engelbreit's Home Companion          5259    189        9048        4363
##  7 Official Xbox Magazine                    5838    542.       4311       10320
##  8 Weight Watchers                           6986    287.       9202        4048
##  9 Globe                                     7634    380        2180       63771
## 10 PSM: 100% Independent PlayStation 2~      8034    720.       6846        5271
## # ... with 194 more rows
```


```r
read_csv("http://gattonweb.uky.edu/sheather/book/docs/datasets/magazines.csv")
```

```
## Parsed with column specification:
## cols(
##   Magazine = col_character(),
##   AdRevenue = col_double(),
##   AdPages = col_double(),
##   SubRevenue = col_double(),
##   NewsRevenue = col_double()
## )
```

```
## # A tibble: 204 x 5
##    Magazine                             AdRevenue AdPages SubRevenue NewsRevenue
##    <chr>                                    <dbl>   <dbl>      <dbl>       <dbl>
##  1 Weekly World News                         2280    300         854       16568
##  2 National Examiner                         3382    380         968       27215
##  3 J-14                                      4218    250        2206       12453
##  4 Soap Opera Weekly                         4622    439        5555       24282
##  5 Easyriders                                5121    524.       4155        9929
##  6 Mary Engelbreit's Home Companion          5259    189        9048        4363
##  7 Official Xbox Magazine                    5838    542.       4311       10320
##  8 Weight Watchers                           6986    287.       9202        4048
##  9 Globe                                     7634    380        2180       63771
## 10 PSM: 100% Independent PlayStation 2~      8034    720.       6846        5271
## # ... with 194 more rows
```


```r
dir.create(here::here("data", "s008_data"), recursive = TRUE)
```

```
## Warning in dir.create(here::here("data", "s008_data"), recursive =
## TRUE): 'C:\Users\Khalia\Documents\GitHub\DataSci-participation\Datasci-
## participation\data\s008_data' already exists
```


```r
xls_url <- "http://gattonweb.uky.edu/sheather/book/docs/datasets/GreatestGivers.xls"
download.file(xls_url, here::here("data", "s008_data", "some_file.xls"), mode = "wb")
```


```r
file_name <- basename(xls_url)
download.file(xls_url, here::here("data", "s008_data", file_name), mode = "wb")
```


```r
read_excel(here::here("data", "s008_data", file_name))
```

```
## # A tibble: 50 x 8
##    Rank  Name  Background `2003-07 Given ~ Causes `Estimated lift~ `Net Worth`
##    <chr> <chr> <chr>      <chr>            <chr>             <dbl> <chr>      
##  1 1     Warr~ Berkshire~  40,650          Healt~            40780 52000      
##  2 2     Bill~ Microsoft~  3,519           Globa~            28144 59000      
##  3 3     Geor~ Oil and g~  2,271           Pover~             2522 11000      
##  4 4     Geor~ Investor    2,109           Open ~             6401 8800       
##  5 5     Gord~ Intel co-~  2,067           Envir~             7404 4500       
##  6 6     Walt~ Family of~  1,475           Educa~             2015 82500      
##  7 7     Herb~ Golden We~  1,368           Medic~             1389 2400       
##  8 8     Eli ~ SunAmeric~  1,216           Publi~             2286 7000       
##  9 9     Dona~ Real esta~  915             Educa~             1326 13000      
## 10 10    Jon ~ Huntsman ~  800             Cance~             1233 1900       
## # ... with 40 more rows, and 1 more variable: `Giving%` <chr>
```


```r
(clevel <- haven::read_spss(here::here("data", "s008_data", "clevel.sav")))
```

```
## # A tibble: 200 x 9
##    id    language  gender isClevel Extraversion EX_Leading EX_Communion
##    <chr> <dbl+lb> <dbl+l>    <dbl>        <dbl>      <dbl>        <dbl>
##  1 34787   3 [NL] 2 [Fem~        0            8          8            7
##  2 2715    2 [FR] 1 [Mal~        0            4          5            4
##  3 33503   3 [NL] 1 [Mal~        0            5          6            3
##  4 23258   3 [NL] 1 [Mal~        0            5          6            3
##  5 27671   3 [NL] 1 [Mal~        0            4          5            4
##  6 4185    2 [FR] 1 [Mal~        0            9          9            9
##  7 33041   3 [NL] 1 [Mal~        0            3          3            3
##  8 43431   3 [NL] 2 [Fem~        0            4          3            6
##  9 7766    3 [NL] 1 [Mal~        0            5          7            1
## 10 22899   3 [NL] 1 [Mal~        0            4          3            6
## # ... with 190 more rows, and 2 more variables: EX_Persuasive <dbl>,
## #   EX_Motivating <dbl>
```


```r
clevel_cleaned <-
  clevel %>% 
  mutate(language = as_factor(language),
         gender = as_factor(gender),
         isClevel = factor(isClevel, 
                           levels = c(0, 1), 
                           labels = c("No", "Yes"))
  ) %>% 
  print()
```

```
## # A tibble: 200 x 9
##    id    language gender isClevel Extraversion EX_Leading EX_Communion
##    <chr> <fct>    <fct>  <fct>           <dbl>      <dbl>        <dbl>
##  1 34787 NL       Female No                  8          8            7
##  2 2715  FR       Male   No                  4          5            4
##  3 33503 NL       Male   No                  5          6            3
##  4 23258 NL       Male   No                  5          6            3
##  5 27671 NL       Male   No                  4          5            4
##  6 4185  FR       Male   No                  9          9            9
##  7 33041 NL       Male   No                  3          3            3
##  8 43431 NL       Female No                  4          3            6
##  9 7766  NL       Male   No                  5          7            1
## 10 22899 NL       Male   No                  4          3            6
## # ... with 190 more rows, and 2 more variables: EX_Persuasive <dbl>,
## #   EX_Motivating <dbl>
```


```r
write_csv(clevel_cleaned, here::here("data", "s008_data", "clevel_cleaned.csv"))
```


```r
clevel_plot <-
  clevel_cleaned %>% 
  mutate(isClevel = recode(isClevel, 
                           No = "Below C-level", 
                           Yes = "C-level"),
         gender = recode(gender,
                         Female = "Women",
                         Male = "Men")) %>% 
  ggplot(aes(paste(isClevel, gender, sep = "\n"), Extraversion, color = gender)) +
  geom_boxplot() +
  geom_jitter(height = .2) +
  scale_color_manual(values = c("#1b9e77", "#7570b3")) +
  ggtitle("Extraversion Stan Scores") +
  scale_y_continuous(breaks = 1:9) +
  ggthemes::theme_fivethirtyeight() %>% 
  print()
```

```
## List of 67
##  $ line                      :List of 6
##   ..$ colour       : chr "black"
##   ..$ size         : num 0.545
##   ..$ linetype     : num 1
##   ..$ lineend      : chr "butt"
##   ..$ arrow        : logi FALSE
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_line" "element"
##  $ rect                      :List of 5
##   ..$ fill         : Named chr "#F0F0F0"
##   .. ..- attr(*, "names")= chr "Light Gray"
##   ..$ colour       : logi NA
##   ..$ size         : num 0.545
##   ..$ linetype     : num 0
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_rect" "element"
##  $ text                      :List of 11
##   ..$ family       : chr "sans"
##   ..$ face         : chr "plain"
##   ..$ colour       : Named chr "#3C3C3C"
##   .. ..- attr(*, "names")= chr "Dark Gray"
##   ..$ size         : num 12
##   ..$ hjust        : num 0.5
##   ..$ vjust        : num 0.5
##   ..$ angle        : num 0
##   ..$ lineheight   : num 0.9
##   ..$ margin       : 'margin' num [1:4] 0pt 0pt 0pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : logi FALSE
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.title.x              :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : NULL
##   ..$ vjust        : num 1
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 3pt 0pt 0pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.title.x.top          :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : NULL
##   ..$ vjust        : num 0
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 0pt 3pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.title.y              :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : NULL
##   ..$ vjust        : num 1
##   ..$ angle        : num 90
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 3pt 0pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.title.y.right        :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : NULL
##   ..$ vjust        : num 0
##   ..$ angle        : num -90
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 0pt 0pt 3pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.text                 :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : 'rel' num 0.8
##   ..$ hjust        : NULL
##   ..$ vjust        : NULL
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : NULL
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.text.x               :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : NULL
##   ..$ vjust        : num 1
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 2.4pt 0pt 0pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.text.x.top           :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : NULL
##   ..$ vjust        : num 0
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 0pt 2.4pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.text.y               :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : num 1
##   ..$ vjust        : NULL
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 2.4pt 0pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.text.y.right         :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : num 0
##   ..$ vjust        : NULL
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 0pt 0pt 2.4pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ axis.ticks                : list()
##   ..- attr(*, "class")= chr [1:2] "element_blank" "element"
##  $ axis.ticks.length         : 'unit' num 3pt
##   ..- attr(*, "valid.unit")= int 8
##   ..- attr(*, "unit")= chr "pt"
##  $ axis.ticks.length.x       : NULL
##  $ axis.ticks.length.x.top   : NULL
##  $ axis.ticks.length.x.bottom: NULL
##  $ axis.ticks.length.y       : NULL
##  $ axis.ticks.length.y.left  : NULL
##  $ axis.ticks.length.y.right : NULL
##  $ axis.line                 : list()
##   ..- attr(*, "class")= chr [1:2] "element_blank" "element"
##  $ axis.line.x               : NULL
##  $ axis.line.y               : NULL
##  $ legend.background         :List of 5
##   ..$ fill         : NULL
##   ..$ colour       : logi NA
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_rect" "element"
##  $ legend.margin             : 'margin' num [1:4] 6pt 6pt 6pt 6pt
##   ..- attr(*, "valid.unit")= int 8
##   ..- attr(*, "unit")= chr "pt"
##  $ legend.spacing            : 'unit' num 12pt
##   ..- attr(*, "valid.unit")= int 8
##   ..- attr(*, "unit")= chr "pt"
##  $ legend.spacing.x          : NULL
##  $ legend.spacing.y          : NULL
##  $ legend.key                :List of 5
##   ..$ fill         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_rect" "element"
##  $ legend.key.size           : 'unit' num 1.2lines
##   ..- attr(*, "valid.unit")= int 3
##   ..- attr(*, "unit")= chr "lines"
##  $ legend.key.height         : NULL
##  $ legend.key.width          : NULL
##  $ legend.text               :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : 'rel' num 0.8
##   ..$ hjust        : NULL
##   ..$ vjust        : NULL
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : NULL
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ legend.text.align         : NULL
##  $ legend.title              :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : num 0
##   ..$ vjust        : NULL
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : NULL
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ legend.title.align        : NULL
##  $ legend.position           : chr "bottom"
##  $ legend.direction          : chr "horizontal"
##  $ legend.justification      : chr "center"
##  $ legend.box                : chr "vertical"
##  $ legend.box.margin         : 'margin' num [1:4] 0cm 0cm 0cm 0cm
##   ..- attr(*, "valid.unit")= int 1
##   ..- attr(*, "unit")= chr "cm"
##  $ legend.box.background     : list()
##   ..- attr(*, "class")= chr [1:2] "element_blank" "element"
##  $ legend.box.spacing        : 'unit' num 12pt
##   ..- attr(*, "valid.unit")= int 8
##   ..- attr(*, "unit")= chr "pt"
##  $ panel.background          :List of 5
##   ..$ fill         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_rect" "element"
##  $ panel.border              :List of 5
##   ..$ fill         : logi NA
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_rect" "element"
##  $ panel.spacing             : 'unit' num 6pt
##   ..- attr(*, "valid.unit")= int 8
##   ..- attr(*, "unit")= chr "pt"
##  $ panel.spacing.x           : NULL
##  $ panel.spacing.y           : NULL
##  $ panel.grid                :List of 6
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ lineend      : NULL
##   ..$ arrow        : logi FALSE
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_line" "element"
##  $ panel.grid.minor          : list()
##   ..- attr(*, "class")= chr [1:2] "element_blank" "element"
##  $ panel.ontop               : logi FALSE
##  $ plot.background           :List of 5
##   ..$ fill         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_rect" "element"
##  $ plot.title                :List of 11
##   ..$ family       : NULL
##   ..$ face         : chr "bold"
##   ..$ colour       : NULL
##   ..$ size         : 'rel' num 1.5
##   ..$ hjust        : num 0
##   ..$ vjust        : num 1
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 0pt 6pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ plot.subtitle             :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : num 0
##   ..$ vjust        : num 1
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 0pt 0pt 6pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ plot.caption              :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : 'rel' num 0.8
##   ..$ hjust        : num 1
##   ..$ vjust        : num 1
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 6pt 0pt 0pt 0pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ plot.tag                  :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : 'rel' num 1.2
##   ..$ hjust        : num 0.5
##   ..$ vjust        : num 0.5
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : NULL
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ plot.tag.position         : chr "topleft"
##  $ plot.margin               : 'unit' num [1:4] 1lines 1lines 1lines 1lines
##   ..- attr(*, "valid.unit")= int 3
##   ..- attr(*, "unit")= chr "lines"
##  $ strip.background          :List of 5
##   ..$ fill         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_rect" "element"
##  $ strip.placement           : chr "inside"
##  $ strip.text                :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : 'rel' num 0.8
##   ..$ hjust        : NULL
##   ..$ vjust        : NULL
##   ..$ angle        : NULL
##   ..$ lineheight   : NULL
##   ..$ margin       : 'margin' num [1:4] 4.8pt 4.8pt 4.8pt 4.8pt
##   .. ..- attr(*, "valid.unit")= int 8
##   .. ..- attr(*, "unit")= chr "pt"
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ strip.text.x              : NULL
##  $ strip.text.y              :List of 11
##   ..$ family       : NULL
##   ..$ face         : NULL
##   ..$ colour       : NULL
##   ..$ size         : NULL
##   ..$ hjust        : NULL
##   ..$ vjust        : NULL
##   ..$ angle        : num -90
##   ..$ lineheight   : NULL
##   ..$ margin       : NULL
##   ..$ debug        : NULL
##   ..$ inherit.blank: logi TRUE
##   ..- attr(*, "class")= chr [1:2] "element_text" "element"
##  $ strip.switch.pad.grid     : 'unit' num 3pt
##   ..- attr(*, "valid.unit")= int 8
##   ..- attr(*, "unit")= chr "pt"
##  $ strip.switch.pad.wrap     : 'unit' num 3pt
##   ..- attr(*, "valid.unit")= int 8
##   ..- attr(*, "unit")= chr "pt"
##  $ axis.title                : list()
##   ..- attr(*, "class")= chr [1:2] "element_blank" "element"
##  $ panel.grid.major          :List of 6
##   ..$ colour       : Named chr "#D2D2D2"
##   .. ..- attr(*, "names")= chr "Medium Gray"
##   ..$ size         : NULL
##   ..$ linetype     : NULL
##   ..$ lineend      : NULL
##   ..$ arrow        : logi FALSE
##   ..$ inherit.blank: logi FALSE
##   ..- attr(*, "class")= chr [1:2] "element_line" "element"
##  - attr(*, "class")= chr [1:2] "theme" "gg"
##  - attr(*, "complete")= logi TRUE
##  - attr(*, "validate")= logi TRUE
```


```r
dir.create(here::here("output", "figures"))
```

```
## Warning in dir.create(here::here("output", "figures")): 'C:
## \Users\Khalia\Documents\GitHub\DataSci-participation\Datasci-
## participation\output\figures' already exists
```

```r
ggsave(here::here("output", "figures", "clevel_extraversion.svg"), clevel_plot)
```

```
## Saving 7 x 5 in image
```

```
## Warning: package 'gdtools' was built under R version 3.6.3
```


```r
ggsave(here::here("output", "figures", "clevel_extraversion.eps"), clevel_plot)
```

```
## Saving 7 x 5 in image
```

```r
ggsave(here::here("output", "figures", "clevel_extraversion.pdf"), clevel_plot)
```

```
## Saving 7 x 5 in image
```

```r
ggsave(here::here("output", "figures", "clevel_extraversion.tiff"), clevel_plot)
```

```
## Saving 7 x 5 in image
```

```r
ggsave(here::here("output", "figures", "clevel_extraversion.png"), clevel_plot)
```

```
## Saving 7 x 5 in image
```


```r
rio::import("clevel.sav", setclass = "tibble", format("sav"))
```

```
## Error in rio::import("clevel.sav", setclass = "tibble", format("sav")): No such file
```

