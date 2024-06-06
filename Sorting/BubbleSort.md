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

