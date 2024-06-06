# Selection Sort

Selection sort is a simple and efficient sorting algorithm that works by repeatedly selecting the smallest (or largest) element from the unsorted portion of the list and moving it to the sorted portion of the list. 
The algorithm repeatedly selects the smallest (or largest) element from the unsorted portion of the list and swaps it with the first element of the unsorted part. This process is repeated for the remaining unsorted portion until the entire list is sorted.

### Complexity Analysis of Selection Sort

  * Time Complexity: The time complexity of Selection Sort is O(N2) as there are two nested loops:
                     One loop to select an element of Array one by one = O(N)
                     Another loop to compare that element with every other Array element = O(N)
                     Therefore overall complexity = O(N) * O(N) = O(N*N) = O(N2)
  * Auxiliary Space: O(1) as the only extra memory used is for temporary variables while swapping two values in Array. The selection sort never makes more than O(N) swaps and can be useful when memory writing is costly.

    <img width="337" alt="image" src="https://github.com/Malobika8/GitDemo/assets/111234135/d4b0ac3e-e8ec-4df7-8781-7a64a0df99d2">


 
        int nums[]={7,8,3,1,2};
        for(int i=0;i<nums.length-1;i++){
            int smallest=i;
            for(int j=i+1;j<nums.length;j++){
                if(nums[j]<nums[smallest]){
                    smallest=j;
                }
            }
            int temp=nums[smallest];
            nums[smallest]=nums[i];
            nums[i]=temp;
        }
        System.out.println(Arrays.toString(nums));

    Output: [1, 2, 3, 7, 8]
