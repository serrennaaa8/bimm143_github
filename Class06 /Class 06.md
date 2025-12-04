# Class 6: R functions
Serena (PID: A18556865

All functions in R have at least 3 things:

- A **name**, we pick this and use it to call the function.
- Input **arguments**, there can be multiple comma separated inputs to
  the function.
- The **body**, lines of R code that do the work of the function.

Our first wee function:

``` r
add <- function(x, y=1){
  x + y 
}
```

Let’s test our first function

``` r
add(c(1,2,3), y=10)
```

    [1] 11 12 13

``` r
add(10)
```

    [1] 11

``` r
add(10,100)
```

    [1] 110

## A second function

Let’s try something more interesting. Make a sequence generation tool.

The `sample()` function could be useful here

``` r
sample(1:10, size = 3)
```

    [1] 3 5 6

Change this to work with nucleotides A C G and T and return 3 of them

``` r
n <- c("A", "C", "G", "T")
sample(n, size = 15, replace = TRUE)
```

     [1] "C" "A" "T" "T" "A" "A" "A" "G" "T" "A" "A" "T" "C" "T" "T"

Turn this snipet into a function that returns a user specified length
duo sequence. Let’s call it `generate_dna()`…

``` r
generate_dna <- function(len=10, fasta = FALSE) {
  n <- c("A", "C", "G", "T")
  v <- sample(n, size = len, replace = TRUE)
  
  # Make a single element vector 
  s <- paste(v, collapse = "")
  
  cat("Well done you!\n")
  
  if(fasta) {
    return(s)
  } else{
    return(v)
  }
}
```

``` r
generate_dna(5)
```

    Well done you!

    [1] "A" "G" "C" "C" "G"

``` r
s <- generate_dna(15)
```

    Well done you!

``` r
s
```

     [1] "G" "G" "T" "G" "C" "G" "G" "C" "A" "G" "C" "T" "C" "C" "A"

I want the option to return a single element character vector with my
sequence all together like this: “GGAGTAC”

``` r
generate_dna(10, fasta = FALSE)
```

    Well done you!

     [1] "G" "T" "C" "G" "A" "G" "G" "C" "T" "C"

## A more advanced example

Make a third function that generates protein sequence of a user specific
length and format

``` r
generate_protein <- function(size= 15, fasta=TRUE) {
  aa <- c(
    "A","R","N","D","C","E","Q","G","H","I",
    "L","K","M","F","P","S","T","W","Y","V")
  
  seq <- sample(aa, size= size, replace = TRUE)
  
  if (fasta) {
    return(paste(seq,collapse = ""))   
  } else {
    return(seq)
  }
}
```

Try this out…

``` r
generate_protein(10)
```

    [1] "HYERYDMQTK"

> Q.Generate random protein sequences between lengths 5 and 12
> amino-acids.

``` r
generate_protein(5)
```

    [1] "FMIGP"

``` r
generate_protein(6)
```

    [1] "AHEHCC"

One approach is to do this by brute force calling our function for each
length 5 to 12.

Another approach is to write a `for()` loop to itterate over the input
valued 5 to 12

A very useful third R specific approach is to use the `sapply()`
function.

``` r
seq_lengths <- 6:12
for (i in seq_lengths) {
  cat(">", i, "\n")
  cat(generate_protein(i))
  cat("\n")
}
```

    > 6 
    RYFEIQ
    > 7 
    PFYDWNV
    > 8 
    FWAFLNGA
    > 9 
    NIEFTTIEL
    > 10 
    CQGMRATSQE
    > 11 
    RMDSKHTARLY
    > 12 
    QLRKPMHCNPVT

``` r
sapply(5:12, generate_protein)
```

    [1] "FEEPH"        "KQHCAS"       "KQYQNWC"      "WPNCTRNW"     "VVFMEWFPA"   
    [6] "RPVGGMKNRA"   "ASVWPPICYCQ"  "QIYGTCITWVIG"

> **Key-Point**: Writing functions in R is doable but not the easiest
> thing in the world. Starting with a working snippet of code and then
> using LLM tools to improve and generalize your function code is a
> productive approach.
