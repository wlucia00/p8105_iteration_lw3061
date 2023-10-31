iteration_list
================
Lucia Wang
2023-10-31

## lists

lists can be useful to store data, and for loops can be used to write
over them - use functions.

lists can contain anything! even a list. -\> essentially a data frame?

main thing is it has an index

Recall:

``` r
vec_numeric = 1:4
vec_char = c("My", "name", "is", "Jeff")

tibble(num = vec_numeric,
       char = vec_char)
```

    ## # A tibble: 4 × 2
    ##     num char 
    ##   <int> <chr>
    ## 1     1 My   
    ## 2     2 name 
    ## 3     3 is   
    ## 4     4 Jeff

what if you add stuff with different lengths - cant put df together, but
you can make a list

``` r
l = list(
  vec_numeric = 1:5,
  vec_char = LETTERS,
  matrix = matrix(1:10, nrow=5, ncol=2),
  summary = summary(rnorm(100))
)
```

accessing lists with \$ or \[\[\]\]

``` r
l$vec_char 
```

    ##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
    ## [20] "T" "U" "V" "W" "X" "Y" "Z"

``` r
l[[2]]
```

    ##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
    ## [20] "T" "U" "V" "W" "X" "Y" "Z"

``` r
l[["summary"]]
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -2.3804 -0.5901  0.4837  0.2452  0.9004  2.4771

## for loops

``` r
list_norm_samples = list(
  a = rnorm(20,1,5),
  b= rnorm(20, 0, 7),
  c= rnorm(20, 20, 1),
  d = rnorm(20, -45, 13)
)

# recall mean and sd fn from last class...
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Argument x should be numeric")
  } else if (length(x) == 1) {
    stop("Cannot be computed for length 1 vectors")
  }
  
  mean_x = mean(x)
  sd_x = sd(x)

  tibble(
    mean = mean_x, 
    sd = sd_x
  )
}
```

you could do it individually.. but its annoying

``` r
mean_and_sd(list_norm_samples$a)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.25  4.92

``` r
mean_and_sd(list_norm_samples$b)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.690  9.30

loop over the list instead

``` r
output = vector("list", length = 4)

for (i in 1:4) {
  output[[i]] = mean_and_sd(list_norm_samples[[i]])
}
```

## map

`map()` does the same thing as for loop with basic structure
`output = map(input, f)`. easier to read but same thing
