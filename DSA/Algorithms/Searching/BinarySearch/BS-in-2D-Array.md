## Searching in Matrices

<img width="1024" alt="Screenshot 2024-06-19 at 10 09 46 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cefc6ffe-56bc-4c8d-b642-a9eb6294ba0e">

*Note: In matrix related question when we are trying to reduce the search space, we have to think about how we cam eliminate rows and columns.*

- Time Complexity: O(logn + logm) (for nXm Matrix)
- Space Complexity: O(1)

1) Row and Column wise Sorted

   <img width="1024" alt="Screenshot 2024-06-19 at 10 11 26 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ce12c206-6509-40a9-a942-a6622d613043">

  - Smallest element in a Row is the first element in first Column
  - Largest element in a Row is the last element in last Column
  - **We need to start searching from 0th Row and last Column**
  - We can compare target with largest(last) element of a Row and if target is smaller then last Column altogether can be ignored as rest of the items downwards
    will be even larger
  - We can compare target with smallest(first) element of a Column and if target is greater, then first Row altogether can be ignored as rest of the items 
    in the left will be smaller

    <img width="952" alt="Screenshot 2024-06-19 at 10 39 19 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/80e1929b-4a42-4fc5-b322-664347e27724">

2) Search in a sorted Matrix

   <img width="1022" alt="Screenshot 2024-06-19 at 10 40 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7b0903c2-72f4-40b8-9c2e-dc418065b8fa">
   <img width="1022" alt="Screenshot 2024-06-19 at 10 41 03 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/abde6b9b-4c70-455f-9ee9-e598457fc826">

   - **Approach is similar to the previous one**

     <img width="936" alt="Screenshot 2024-06-19 at 11 10 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/572d7b39-c60b-46c0-b2cf-2f11787efe79">

   - **Using Binary Search**

         static int[] search2(int[][] arr, int target) {
          int n = arr.length, m = arr[0].length;

          // apply BS on the last column, this way we can reduce the no of rows in which
          // we want to apply BS to just 1.
          int lb = 0, ub = n - 1, mid;

          while (lb < ub) {
            mid = lb + (ub - lb) / 2;

            if (arr[mid][m - 1] < target) {
                lb = mid + 1;
            }
            else if (arr[mid][m - 1] > target) {
                ub = mid;
            }
            else {
                return new int[] { mid, m - 1 };
            }
          }

          // here lb == rb

          int ind = binarySearch(arr[lb], target);

          if (ind != -1)
            return new int[] { lb, ind };

          return new int[] { -1, -1 };
          }

  ## Notes

  https://github.com/Malobika8/DSA-Bootcamp-Java/tree/main/lectures/10-binary%20search
