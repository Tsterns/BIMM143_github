# R Functions Lab Class_06
Tessa Sterns PID:18482353

Every function in R contain at least 3 things:

- A **name** that we choose.
- Input **arguments**, multiple possible seperated by a comma.
- The **body**, lines of R code that do the work of the function.

My first lil function;

``` r
add <- function(x, y = 5) {x + y}

add(10)
```

    [1] 15

``` r
add(10,20)
```

    [1] 30

``` r
add(c(1,2,3), 2)
```

    [1] 3 4 5

## The Second Function!

A sequence generator The `sample()` function can be useful in this

``` r
sample(1:10, size = 3)
```

    [1] 7 6 4

``` r
sample(c("A", "G", "T", "C"), size = 20, replace = TRUE)
```

     [1] "G" "A" "A" "C" "A" "A" "A" "C" "C" "G" "C" "A" "G" "A" "G" "T" "T" "T" "G"
    [20] "G"

``` r
DNA_Generator <- function( b=10 ) {
  v <- sample(c("A", "G", "T", "C"), size = b, replace = TRUE) 
  cat("Good Job\n")
  return(v)}
DNA_Generator(30)
```

    Good Job

     [1] "A" "G" "A" "G" "A" "T" "T" "A" "A" "G" "G" "G" "G" "A" "G" "A" "T" "A" "G"
    [20] "A" "A" "G" "G" "A" "C" "C" "T" "A" "A" "A"

``` r
DNA_Generator()
```

    Good Job

     [1] "G" "C" "T" "T" "C" "C" "A" "T" "A" "G"

``` r
s <- DNA_Generator(20)
```

    Good Job

``` r
s
```

     [1] "G" "C" "C" "G" "T" "T" "A" "G" "C" "A" "A" "A" "C" "A" "G" "T" "T" "T" "A"
    [20] "T"

I want the option to return a single element vector “TATTAA” The
`paste0()` with collapse = “” will reduce a vector down to a single
element.

``` r
DNA_Generator2 <- function( b=10, type = c("multi", "fasta")) {
  type <- match.arg(type)
  v <- sample(c("A", "G", "T", "C"), size = b, replace = TRUE) 

  ## single element vector
  cat("Good Job\n")
  if (type == "fasta") {
    return(paste0(v, collapse = ""))
  } else {
    # Return the vector of individual bases
    return(v)
  }
}
DNA_Generator2(40, "fasta")
```

    Good Job

    [1] "CCGGCAATCAGACATCCAGAATTTTCTCCTTCTGTGGTGT"

Protein sequence generator

``` r
Protein_Gen <- function( b=10, type = c("PolyP", "multi")) 
  ## make the defult return the first argument in type()
  {
  type <- match.arg(type)
  
  AA <- sample(c("A","R", "N", "D", "Q", "H", "I",
                 "E", "G", "T", "C", "L", "K", "M",
                 "F", "P", "S", "W", "Y", "V"),
               size = b, replace = TRUE) 
 
  ## single element vector
 
  if (type == "multi") {
    return(AA)
  P} else {
    # Return the vector of individual bases
    return(paste0(AA, collapse = ""))
  }
}
Protein_Gen(37, "multi")
```

     [1] "D" "G" "K" "Y" "F" "H" "R" "I" "F" "T" "G" "C" "L" "L" "N" "R" "S" "Y" "R"
    [20] "F" "R" "M" "F" "E" "Q" "Q" "W" "F" "V" "H" "P" "M" "S" "M" "Y" "I" "Q"

``` r
Protein_Gen(65)
```

    [1] "GWICEYASRRFACYCQLGNIFACNENQENWPGPFEREDCKKWCGQMRMYTLSSNCKVHYSVFDSY"

> Q. Generate random protein sequences between length 5 and 12
> amino-acids.

``` r
sapply(5:12, Protein_Gen)  |> cat(sep = "\n")
```

    WMNMC
    AIDYGY
    GRECPYA
    CNKQCIVT
    LQLCYCADI
    TSKVCAVATH
    GTHKYWDGRRC
    LINTHKEKVHAH

> **Key-Point**: writting functions in R is doable but not always
> intuitive. Starting with a working portion of code and using LLM tools
> to modify it can generate a more robust working function.
