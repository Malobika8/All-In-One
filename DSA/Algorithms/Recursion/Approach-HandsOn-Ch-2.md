### Basic Questions

#### Note:
- We should always try to find *Recurrence Relation*
- Base condition is the answer that al already provided to us
- *MAKE SURE TO RETURN THE RESULT OF A FUNCTION CALL OF THE RETURN TYPE*

#### Types of Recurrence Relations
- Linear Recurrence Relation (Ex: Fibonacci) (This is actually very in-efficient)
- Divide & Conquer Recurrence Relation (Ex: Binary Search)

#### How to understand and approach a problem
- Identify if you can breakdown problem into smaller problems
- Write the Recurrence relation if needed
- Draw the Recursive Tree
- About the Tree:
  - See the flow of functions i.e. how they are getting in Stack
  - Identify and focus on left tree calls and right tree calls
  - Draw the tree and pointers again and again using pen & paper
  - Use a Debugger to see the flow
- See how the values and what type of values are returned at each step. See where the function call will come out. In the end, you will come
  out of the main function

#### Key areas
- Arguments
- Base condition
- Recurrence Relation
- What to return? / Return type

#### 1. Fibonacci Series - Print nth term

Recurrence Relation: f(n) = f(n-1) + f(n-2)

<img width="1022" alt="Screenshot 2024-07-03 at 9 30 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b276d799-0a90-480e-8046-dd3a9a5b37f9">
<img width="1016" alt="Screenshot 2024-07-03 at 9 30 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/af5b39d3-0b21-4493-b581-45f1cb70b1ac">

```
public static int fibo(int n){
        if(n < 2){
            return n;
        }
        return fibo(n-1)+fibo(n-2); MAKE SURE TO RETURN THE RESULT OF A FUNCTION CALL OF THE RETURN TYPE*
    }
```

#### 2. Binary Search

Recurrence Relation: f(n) = O(1)(Comparison) + f(n/2)(Dividing Array in half)

```
public static boolean bs(int target, int[] arr, int low, int high){

        if(high<low)
            return false;

        int mid=low + (high-low)/2;

        if(target == arr[mid])
            return true;
        
        if(target<arr[mid])
            return bs(target,arr, low, mid-1); //MAKE SURE TO RETURN THE RESULT OF A FUNCTION CALL OF THE RETURN TYPE*
        
        return bs(target, arr, mid+1, high); //MAKE SURE TO RETURN THE RESULT OF A FUNCTION CALL OF THE RETURN TYPE*
    }
```




