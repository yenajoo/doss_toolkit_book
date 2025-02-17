


# Coding style

*Written by Marija Pejcinovska and last updated on 5 February, 2022.*

## Introduction 

By now you've probably worked through dozens of modules and are feeling a lot more comfortable coding in R. This is a good spot to spend a moment or two thinking about your coding style. A good style will help you keep your R scripts consistent and easy to read (and, of course, much easier to navigate through when you revisit them at a later time).  

In this lesson we'll focus on the coding style used throughout the `tidyverse`. More specifically, we will highlight some naming conventions for objects and functions and discuss useful structures that will make your programs easier to write and read.


Prerequisite skills include:

- Some data manipulation
- The tidyverse
- Writing basic functions and conditional statements 



## Naming things: the tidy way

### Naming files 

In a previous lesson you learned how to set up folders and organize files in your R projects. Here we'll talk about a few things you might want to keep in mind when naming your R files.  

  * Make sure your files have meaningful (though, if possible, also relatively short) names that end in `.R`. 
  * Try sticking to a specific capitalization. The tidyverse style recommends using lower case letters.
  * Avoid spaces and special characters. Consider separating words in a file name by using `_` or `-`. 



```r

# A good example of file name
my_first_script.R

# And a few bad (and less than ideal) examples
my first script.R     # there should be no spaces
myfirstscript.R       # not a terrible file name but hard to read 
my_first_script.r     # r should be capitalized
file1.R               # not descriptive enough
models&results.R      # contains special characters

```


### Naming objects

Just like with file names, you should name your R objects using descriptive and informative names. Here are some guidelines to keep in mind:

  - Object and function names must start with a letter (and not a number)!

```r
# Good 
group_1
# Also good
group_one

# Bad 
1st_group
```
  
  - Names should include only letters, numbers, `_`, or `.`. Though, you should probably decide on a single separator; pick either `_` or `.` to be somewhat consistent and follow basic conventions.
  - Since classes and methods in the S3 object system use dots, to avoid confusion, it might be best to use `_` in your function names. In fact, the tidy style guide, in general, recommends using `_` to separate words both in function names and object names. Separating lowercase words with `_` is sometimes referred to as using *snake_case*.
  - To avoid errors, names should be kept as short as possible.
  - When naming your functions consider using active verbs. For instance, 
  

```r
# Okay function names
permute()
count_event()

# Less okay
permuatation()
event_counter()

```

  - Typos and cases matter; so, be careful when calling your objects and functions. Sometimes errors in your code could end up being just silly misspellings. 
  - Avoid re-using names of common R functions and variables. For instance, avoid naming objects `T` or `F` since R reserves these for `TRUE` and `FALSE`.
  

  
## Tidying up your "syntax"

### Commas and spaces

Many of the syntax rules in the English language are applicable to R coding. Commas and spaces are a good example of this. 

  - Place spaces after commas, but not before them (just like you would when you write).

```r
# Good 

B[, 2]

# Not so good

B[,2]
B[ ,2]
B[ , 2]

```
  
  - Avoid putting space between your function name and the arguments in parenthesis when calling your function  
  

```r

# Do
sum(x)

# Don't

sum (x)
sum( x )
```
  

  - When using conditional (`if`, `for`, `while`) statements separate the condition expression in `()` by placing space around `()`
  

```r

# Good

while (i < 10) {
  print(i)
}

# Not so good

while(i<10){
  print(i)
}

```
  - *Infixed* operators (i.e. those placed between operands), such as `==`, `+`, `-`, `<-`, and so on, **should always** be surrounded by spaces

```r

# Good
my_var <- y + 24 + (x * 0.5)


# Not great
my_var<-y+24+(x*0.5)
```

  - There are, however, a few exception to the above rule. *Operators with high precedence*, such as those that access stuff in a namespace (`::`, `:::`), those used for extracting slots or components (`$`, `@`), those used for indexing (`[]`, `[[]]`), the exponentiation operator (`^`), or the sequence operator (`:`) *should not* be surrounded by space.
  

```r

# Good
x <- data$height
y <- 1:20
z <- x^2

# Bad
x <- data $ height
y <- 1 : 20
z <- x ^ 2

```
  
### Curly braces and code hierarchies

  - When writing functions and conditional statements which are not short or simple you would need to place your code in a block sectioned off by **curly braces**. Enclosing the "body" of a function or conditional statement inside curly braces allows one to more easily see the hierarchy of a piece of code. There are few things to keep in mind here: 
    + `{` should be the last character on a line. Once you open the left squiggly bracket start the actual body of the code in a new line. 
    + The code content inside the curly braces should be indented by two spaces. This way you'll be able to see the hierarchy of the code block more easily
    + When you are done with specifying the code that defines your function or conditional statement place the closing curly brace on a new line, so that it's the first character on the line. In fact, unless it is followed by `else {`, the closing curly brace should be on its own line.
    

```r
# Good
if (x < 3) {
  exp(x)
} else {
  x^3
}

if (i < 10){
  if (x > 0){
    y = log(x)
  } else {
    y = x
  }
} else {
  message("i is too large")
}


# Not so good
if (x < 3) {
  exp(x)} 
else {
  x^3}

if (i < 10){
  if (x > 0){
    y = log(x)
} else {
    y = x
}
} else {
  message("i is too large")}

```

### Function arguments and assignments  

  - When calling a function, it's good to be familiar with the function's arguments. Most have an argument that supplies the data which is used to perform some calculation. There might, of course, be other arguments that control additional aspects of that calculation. For instance, the `mean` function lists the following arguments `mean(x, trim = 0, na.rm = FALSE, ...)`, where `x` is the data argument. With most functions you might be able to get away with supplying the data without using the default value of the argument (in the case of `mean()` this would mean without explicitly typing `x = ...your data here..`). However, a bit more care should be taken when supplying the other arguments. You should be aware of the order of those arguments and should avoid partial matching.  
  

```r
# Better
mean(x = c(NA,1:10), na.rm = TRUE)

# Also good
mean(c(NA,1:10), na.rm = TRUE) # notice here we omitted supplying the data as x =

# Don't do! 
mean(c(NA,1:10), TRUE) # in fact, this will throw an error — do you see why?
```
  - Avoid making any assignments inside function calls. Where necessary try defining objects outside of your function.  
  


### A note on indentation

Consider using two spaces when indenting your code. This is preferred to using tabs. One thing you should probably avoid is mixing both! In other words, avoid indenting some lines in your code using spaces and others using tabs. 

### Few other notes on syntax

  - Avoid using semicolons (`;`) at the end of a line of code. 
  - Avoid putting multiple commands on one line; hence, avoid using semicolons to separate multiple commands on one line! Multiple commands on a single line make your code cluttered and harder to read. 
  - You can use `<-` or `=` for assignment in R, however, the tidyverse style guide strongly advocates for consistently using `<-` for value assignment.

```r
# Do
my_var <- 7

# Maybe don't do
my_var = 7
```
  - The pipe operator,` %>% `, should be preceded by space and should usually be followed by a new line. Just like indentation in code blocks, the code following a pipe should be indented by two spaces (Side note: if you are working on an R script or an RMarkdown file in RStudio you may have noticed that the indentation on the next line is automatically done for you!).  
  

```r
# Good
data %>%
  filter(x > 10) %>% 
  group_by(my_cat_var) %>% 
  summarize(my_sum = sum(my_other_var)) %>% 
  ungroup()

# Not so good
data %>% filter(x > 10) %>% group_by(my_cat_var) %>% summarize(my_sum = sum(my_other_var)) %>% 
  ungroup()

```
  - Recall that in the `tidyverse` when using the package `ggplot2` layers of your plot are separated by `+` instead of `%>%`. However, the style suggestions remain the same. The `+` operator should be preceded by a space and the code that follows should appear on the next line. It is recommended that if you are incorporating your plot code inside an existing piped code you keep a single level of indentation. It is also customary to add new layers on separate lines. If you write a ggplot layer with too many arguments, for clarity it would be preferable to split this long line and place each argument of you layer in a separate line.   
  - Inside `if()` clauses, use `&&` and `||` instead of the usual logical operators, `&` and `|`.



<!-- ```{r style_q1, echo=FALSE} -->
<!-- question("Which one of these follows the tidy style?", -->
<!--          answer("x<-3"), -->
<!--          answer("x=3"), -->
<!--          answer("x <- 3", correct = TRUE), -->
<!--          answer("x < - 3")) -->
<!-- ``` -->



<!-- ```{r style_q2, echo=FALSE} -->
<!-- question("Select the appropriately styled line of code?", -->
<!--          answer("here::here(\"data/my_file.R\")", correct = TRUE), -->
<!--          answer("here::here (\"data/my_file.R\")"), -->
<!--          answer("here ::here(\"data/my_file.R\")") -->
<!-- ) -->
<!-- ``` -->



## Next Steps

This tutorial is largely based on content in the tidyverse style guide. For more detailed information check out: https://style.tidyverse.org/



## Exercises


### Question 1

Which of these expressions follows the *tidy* style? Select all that apply.  

  a. `x<-3`  
  b. `x=3`  
  c.  `x <- 3`  
  d. `x < - 3`  
  
### Question 2  

Select the appropriately styled line of code from the following choices:    

  a.  `here::here("data/my_file.R")`  
  b. `here::here ("data/my_file.R")`  
  c. `here ::here("data/my_file.R")`  
  d. `here :: here("data/my_file.R")`

### Question 3  

The operator `==` should never be surrounded by space.  

  a. True  
  b.  False


### Question 4  

The following file `statistical analysis.R` follows the *tidy* style?  

  a. True  
  b.  False  

### Question 5  
Suppose you made a function called `normalized_sum` taking on some arguments. When calling your function you should leave space between the function name and the arguments in the parenthesis.  

  a. True   
  b.  False

### Question 6

The following code chunk is in accordance with *tidy* coding practices:  

```r
if (sum > 0) {
  print("It works!")
}
```
  a.  True  
  b. False

### Question 7

Which of the following R object assignments follows the tidy style guide principles:   

  a. `T <- FALSE`  
  b. `c <- 1`
  c. `sum <- mean(1:10)`  
  d.  `a <- 2`  
  e. All of the above  
  f. None of the above
  

### Question 8  

When indenting your code it is okay to use a mix of tabs and spaces.   

  a. True  
  b.  False

### Question 9  


```r
my_function <- function(age = age, total = total, lambda = 0.8,
  prob = 0.3,
  sum = NULL) {
  # Code for some difficult calculation
}
```

Which of the following best describes the reason the above code chunk is not in line with tidy principles?  

  a. The spaces between the function arguments and the code.  
  b.  The indentation of the function arguments.  
  c. None of the above! This function is actually tidy.  
  d. Both a. and b. are the culprits.

### Question 10

Suppose you ran a model and saved your results in an object named `model-1`. You are confident in the naming choice because it is in line with coding practices.   

  a. True  
  b.  False
