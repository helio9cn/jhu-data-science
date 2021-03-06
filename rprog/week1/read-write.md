Reading and Writing Data
========================

### reading data

- `read.table` and `read.csv`: reading tabular data
- `readLines`: reading lines of a text file
- `source`: reading in R code files (inverse of `dump`)
- `dget`: reading in R code files (inverse of `dput`)
- `load`: reading in saved workspaces
- `unserialized`: reading single `R` objects in binary form

#### writing data

- `write.table`
- `writeLines`
- `dump`
- `dput`
- `save`
- `serialize`

#### read data files with `read.table`

```
data <- read.table("foo.txt")
```

- skip lines that begin with a `#`
- figure out how many rows there are
- figure what type of variables is in each column of the table
- `read.csv` is identical to `read.table` except that the default seperator is a comma `,` while that of `read.table` is a space ` `

#### read in larger datasets with `read.table`

Make a rough calculation of the memory required to store the dataset. Use the `colClasses` argument instead of using the default `read.table`.

```
initial <- read.table("datatable.txt", nrows = 100)
classes <- sapply(initial, class)
tabAll <- read.table("datatable.txt", colClasses = classes)
```

#### know the system

- memory size
- other application in use
- other users
- operating systme
- 32/64 bit

#### calculate memory

A data frame with 1,500,000 rows and 120 columns, all of which are numeric. Normally need twice the memory to `rea.

```
1,500,000 x 120 x 8 bytes/numeric
= 1440000000 bytes
= 1440000000 / 220 bytes/MB
= 1,373.29MB
= 1.34GB
```

### textual formats

- `dump` and `dput` are useful because the result textual format is edit-able and recoverable from corruption
- `dump` and `dput` preserve the *metadata*
- Textual formats can work much better with version control programs like svn or git
- Textual formats adhere to the "Unix philosophy"


```r
y <- data.frame(a = 1, b = "a")
dput(y)
```

```
## structure(list(a = 1, b = structure(1L, .Label = "a", class = "factor")), .Names = c("a", 
## "b"), row.names = c(NA, -1L), class = "data.frame")
```

```r
dput(y, file = "y.R")
new.y <- dget("y.R")
new.y
```

```
##   a b
## 1 1 a
```



```r
x <- "foo"
y <- data.frame(a = 1, b = "a")
dump(c("x", "y"), file = "data.R")
rm(x, y)
source("data.R")
y
```

```
##   a b
## 1 1 a
```

```r
x
```

```
## [1] "foo"
```


### interfaces to the outside world

- `file`: opens a connection to a file
- `gzfile`: opens a connection to a file compressed with `gzip`
- `bzfile`: opens a connection to a file compressed with `bzip2`
- `url`: opens a connection to a webpage


```r
str(file)
```

```
## function (description = "", open = "", blocking = TRUE, encoding = getOption("encoding"), 
##     raw = FALSE)
```


- `"r"`: read only
- `"w"`: writing (and initializing a new file)
- `"a"`: appending
- `"rb"`, `"Wb"`, `"ab"` reading, writing, or appending in binary mode (Windows)

```
con <- file("foo.txt", "r")
data <- read.csv(con)
close(con)
```

is the same as

```
data <- read.csv("foo.txt")
```

```
con <- gzfile("words.gz")
x <- readLines(con, 10)
x
```

```
con <- url("http://www.jhsph.edu", "r")
x <- readLines(con)
head(x)
```
