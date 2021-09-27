# Leak report

_Use this document to describe whatever memory leaks
you find in `clean_whitespace.c` and how you might fix
them. You should also probably remove this explanatory
text._

## Write Up

The memory leak in `clean_whitespace.c` is cause by not "freeing" the memory allocation for the `result` variable in the `strip` function. Since this function is called again by the `is_clean` function, and the `main` function does not need to preserve the memory or another operation after printing the result of `is_clean` the memory should be freed in the `is_clean` function. The result of the `strip` function is assigned to the variable `cleaned` inside of the `is_clean` function, so that is the variable that needs to be freed. There are two cases that need to consider because the `strip` function can return two results, either an empty string `""` or Boolean value. These cases can be handled by wrapping `free(cleaned);` inside an conditional that tests if the `strlen(cleaned)` is not equal to `0`. This test ensures that `free(cleaned);` is only called if the `strip` function has allocated memory.