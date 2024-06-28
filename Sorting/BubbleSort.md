# Bubble sort

Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order. This algorithm is not suitable for large data sets as its average and worst-case time complexity is quite high.

### Bubble Sort Algorithm
  * traverse from left and compare adjacent elements and the higher one is placed at right side. 
  * In this way, the largest element is moved to the rightmost end at first. 
  * This process is then continued to find the second largest and place it and so on until the data is sorted.
    
  If there are n number of elements?
  
   * Total no. of passes: n-1
   * Total no. of comparisons: n*(n-1)/2

  **Time Complexity: O(N2)** , 
  **Auxiliary Space: O(1)**

  <img width="762" alt="image" src="https://github.com/Malobika8/GitDemo/assets/111234135/e4d78484-a687-49c2-96de-733ced095892">

        int nums[]={7,8,3,1,2};
        int temp;
        for(int i=0;i<nums.length-1;i++){
            for(int j=0;j<nums.length-i-1;j++){
                if(nums[j]>nums[j+1]){
                    temp=nums[j];
                    nums[j]=nums[j+1];
                    nums[j+1]=temp;
                }
            }
        }
        System.out.println(Arrays.toString(nums));

  **Output:** [1, 2, 3, 7, 8]

  We can have a boolean value which can track if swap is taking place. If no swap occurs for any value of i, it indicates that the array is 
  already sorted.

  <img width="1078" alt="Screenshot 2024-06-28 at 8 29 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b19a908f-c8c5-4b38-a219-641f8bb66ab0">

  ---------------
  
  This is a stable sorting algorithm which means the original order of the values(same values) is maintained.

  Ex: 10(i1), 20(i1), 30(i1), 10(i2)

  Post sorting: The order of 10i1 and 10i2 is maintained.

  10(i1), 10(i2), 20(i1), 30(i1)

