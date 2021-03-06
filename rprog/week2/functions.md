Functions
=========

- functions can be passes as arguments to other functions
- functions can be nested, so you can define a function inside of another function. The return value of a function is the last expression in the function body

```
f <- function(<arguments>) {
  ## do something
}
```

#### argument

- the formal arguments are the arguments included in the function definition
- the `formals` function returns a list of all the formal arguments of a functions
- not every function of `R` makes use of all the formal arguments
function arguments can be missing or might have default values

The following calls to `sd` are all equivalent:

```
mydata <- rnorm(100)
sd(mydata)
sd(x = mydata)
sd(x = mydata, na.rm = FALSE)
sd(na.rm = FALSE, x = mydata)
sd(na.rm=FALSE, mydata)
```

### defining a function


```r
f <- function(a, b = 1, c = 2, d = NULL) {
    
}
```


#### lazy evaluation


```r
f <- function(a, b) {
    a^2
}
f(2)
```

```
## [1] 4
```


> missing `b` doesn't give any error



```r
f <- function(a, b) {
    print(a)
    print(b)
}
f(45)
```

```
## [1] 45
```

```
## Error: 缺少参数"b",也没有缺省值
```


> error was trigger after `print(a)`

#### `"..."` argument

The `...` argument indicate a variable number of arguments that usually passed on to other functions.

```
myplot <- function(x, y, type = "1", ...) {
  plot(x, y, type = type, ...)
}
```

> any arguments that appear *after* `...` on the argument list must be named explicitly and cannot be partially matched


```r
args(paste)
```

```
## function (..., sep = " ", collapse = NULL) 
## NULL
```

```r
paste("a", "b", sep = ":")
```

```
## [1] "a:b"
```

```r
paste("a", "b", se = ":")
```

```
## [1] "a b :"
```

