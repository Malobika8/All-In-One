# Nearest Largest element or Nearest Greater to right

Given an array, print the Next Greater Element (NGE) for every element. 

Note: The Next greater Element for an element x is the first greater element on the right side of x in the array. Elements for which no greater element exist, consider the next greater element as -1. 

Examples: 

Input: arr[] = [ 4 , 5 , 2 , 25 ]
Output:  
```
              4      –>   5
               5      –>   25
               2      –>   25
              25     –>   -1
```

Explanation: Except 25 every element has an element greater than them present on the right side


Input: arr[] = [ 13 , 7, 6 , 12 ]
Output:  
```
                13      –>    -1
                7       –>     12
                6       –>     12
               12      –>     -1
```

Explanation: 13 and 12 don’t have any element greater than them present on the right side
