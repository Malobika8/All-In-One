# Table of Contents

1. [Intro](#general)
2. [To find size of an array by indices](#size)
3. [Ceiling of a given number (Find the smallest number that is greater than or equal to target)](#question1)
4. [Find the floor of a number (Find the largest number that is lesser than or equal to target)](#question2)
5. [Find smallest letter greater than the target](#question3)
6. [Find First and Last Position of Element in Sorted Array](#question4)
7. [Position of an Element in Infinite Sorted Array](#question5)
8. [Peak Index in a Mountain Array (bitonic array)](#question6)
9. [Find in Mountain Array](#question7)
10. [Search in Rotated Sorted Array](#question8)
11. [What if the array contains duplicate values?](#question9)

## How do we know when to apply binary search? <a name="general"></a>
If in the prolem statement, we are given a sorted array, we can try binary search first. Other problem statements include something like we
are required to get one particular answer & we are following a continuous sequence to get that answer.

Eg. sq root of a number

### Note: To find size of an array by indices <a name="size"></a>

<img width="1021" alt="Screenshot 2024-06-17 at 11 53 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2987da0b-1008-4d5c-9ba6-4d7e21d062a8">

## Q1. Ceiling of a given number (Find the smallest number that is greater than or equal to target) <a name="question1"></a>

https://leetcode.com/problems/search-insert-position/

<img width="1142" alt="Screenshot 2024-06-15 at 11 31 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0b3350a5-0d99-4335-a9ec-02fc921e6702">
<img width="1019" alt="Screenshot 2024-06-15 at 12 38 37 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/af90094b-2b99-42e5-8e18-b6e735fbef94">
<img width="1022" alt="Screenshot 2024-06-15 at 12 38 51 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6b90412f-0bff-4544-82fc-e6efbd115996">

<img width="811" alt="Screenshot 2024-06-15 at 12 39 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/11b00982-f1a2-43da-a8d1-5a11c1debf2c">

## Q2. Find the floor of a number (Find the largest number that is lesser than or equal to target) <a name="question2"></a>

<img width="1013" alt="Screenshot 2024-06-15 at 12 45 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ad3293c2-09c7-4cd9-b2ef-12f654270fe9">
<img width="1012" alt="Screenshot 2024-06-15 at 12 46 06 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/67aa98f1-a714-42d3-8d4c-01d883b0ec4b">

Same as above. Consider "end" this time.

## Q3. Find smallest letter greater than the target <a name="question3"></a>

https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/

<img width="1007" alt="Screenshot 2024-06-16 at 12 25 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/03fcb3a4-caeb-4894-a573-9cab153f3bcb">
<img width="1002" alt="Screenshot 2024-06-16 at 12 25 17 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2bcda1ed-6c57-47ff-8380-74023b3e6e71">

<img width="802" alt="Screenshot 2024-06-16 at 12 38 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/24f5f8c4-974c-4571-9160-72394c3190b2">

Or we can also just return "letters[start % letters.length]".

## Q4. Find First and Last Position of Element in Sorted Array <a name="question4"></a>

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/

We can solve this using linear search as well in O(n) time. However, better would be to do using binary search as time would then reduce to 
O(log n).

Run binary search twice - to find first occurrence of target and last occurrence of target

<img width="1018" alt="Screenshot 2024-06-16 at 1 30 04 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f45e6de3-a2f2-4d61-8dbd-c46c16002333">

<img width="763" alt="Screenshot 2024-06-16 at 1 25 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7d41d60b-0685-427f-9e2a-e3d6ec891028">
<img width="814" alt="Screenshot 2024-06-16 at 1 26 27 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ea7b2e17-c74b-42e6-b6b1-7bab5dfd84cf">

## Q5. Position of an Element in Infinite Sorted Array <a name="question5"></a>

https://www.geeksforgeeks.org/find-position-element-sorted-array-infinite-numbers/

<img width="669" alt="Screenshot 2024-06-16 at 1 33 01 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cb8909e0-182f-4af8-b851-959b35de2404">

- Find bound first
- Check for bound till the target is greater than end index of the array
- Run binary search


      public class FindInInfiniteSortedArray {
        public static void main(String[] args) {
          int[] arr = {1,2,4,5,6,7,8,9,12,14,16,17,18,21};
          int target = 18;

          System.out.println(findBoundsAndSearch(arr,target));
        }
  
        public static int findBoundsAndSearch(int[] arr, int target){
        int start=0;
        int end=1;

         while(target>arr[end]){
            int newStart=end+1;
            int size=end-start+1;
            end = end+(2*size);
            start=newStart;
         }

         System.out.println(end);
         System.out.println(start);

         return search(arr, start, end, target);
         }
  
         public static int search(int[] arr, int start, int end, int target){

         while(start<=end){
            int mid=start + (end-start)/2;

            if(target<arr[mid]){
                end=mid-1;
            }
            else if(target>arr[mid]){
                start=mid+1;
            }
            else{
                return mid;
            }
          }
          return -1;
          }
         }

  ## Q6. Peak Index in a Mountain Array (bitonic array) <a name="question6"></a>

  https://leetcode.com/problems/peak-index-in-a-mountain-array/description/

  <img width="1005" alt="Screenshot 2024-06-16 at 8 52 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6ba9ffdd-1669-4a09-a36e-e9dbc9957b1d">
  <img width="1012" alt="Screenshot 2024-06-16 at 8 53 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/24f8ad9a-8ad5-4539-bb3b-e8bc8b90708a">
  <img width="1014" alt="Screenshot 2024-06-16 at 8 53 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8b6607ff-c3b5-426c-99a1-ea64df7c93dd">
  <img width="1015" alt="Screenshot 2024-06-16 at 8 53 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7a25b53b-0fdf-4191-8de1-4b88edf29da1">
  <img width="1012" alt="Screenshot 2024-06-16 at 8 53 39 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7861a747-eaaf-4e97-abc5-52d91337af07">

  <img width="810" alt="Screenshot 2024-06-16 at 8 54 07 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/960d63b5-1d7f-4c9e-b805-00dcf96a5e3c">

  ## Q7. Find in Mountain Array <a name="question7"></a>

  https://leetcode.com/problems/find-in-mountain-array/description/

  <img width="1012" alt="Screenshot 2024-06-17 at 11 58 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5432edc2-60de-44fb-9095-093ba9b63519">

      /**
       * // This is MountainArray's API interface.
       * // You should not implement it, or speculate about its implementation
       * interface MountainArray {
       *     public int get(int index) {}
       *     public int length() {}
       * }
       */
 
      class Solution {
      public int findInMountainArray(int target, MountainArray mountainArr) {
        
        int num;
        boolean front=true;

        int index = peakElementIndex(mountainArr);
        num = binarySearch(target, mountainArr, index, true);

        if(num == -1)
            num = binarySearch(target, mountainArr, index, false);

        return num;
      }
  
      public int peakElementIndex(MountainArray mountainArr){
        int start = 0;
        int end = mountainArr.length()-1;

        while(start<end){

            int mid=start + (end-start)/2;

            if(mountainArr.get(mid+1)<mountainArr.get(mid)){
                end=mid;
            }
            else if(mountainArr.get(mid+1)>mountainArr.get(mid)){
                start=mid+1;
            }
        }
        return start;
      }

      public int binarySearch(int target, MountainArray mountainArr, int index, boolean front){
        int start, end;
        if(front){
            start=0;
            end=index;
        }
        else{
            start=index;
            end=mountainArr.length()-1;
        }
        
        while(start<=end){
            int mid=start + (end-start)/2;

            if(front){
                if(target< mountainArr.get(mid))
                    end=mid-1;
                else if(target> mountainArr.get(mid))
                    start=mid+1;
            }
            else{
                if(target > mountainArr.get(mid))
                    end=mid-1;
                else if(target< mountainArr.get(mid))
                    start=mid+1;
            }

            if(target == mountainArr.get(mid))
                return mid;
        }
        return -1;
      }
      }

  ## Q8. Search in Rotated Sorted Array <a name="question8"></a>

  https://leetcode.com/problems/search-in-rotated-sorted-array/description/

  <img width="1013" alt="Screenshot 2024-06-17 at 1 19 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/059b98f5-748c-4e39-bc21-e21344f0c1f2">
  <img width="1017" alt="Screenshot 2024-06-17 at 1 19 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/db247142-9b78-407d-a7ee-b6d49af12506">
  <img width="1019" alt="Screenshot 2024-06-17 at 1 19 19 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/bbd953fb-4fd7-47bb-9b88-5282e2a0a43e">
  <img width="1018" alt="Screenshot 2024-06-17 at 1 20 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/94232765-350e-4df3-abb4-c257979e73bb">
  <img width="1017" alt="Screenshot 2024-06-17 at 1 20 25 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3fc691ab-09d5-4820-a752-ff04de615b0a">
  <img width="1014" alt="Screenshot 2024-06-17 at 1 20 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0c44412a-3cbb-4e80-80a5-fc1416fa8bc5">
  <img width="1020" alt="Screenshot 2024-06-17 at 1 20 43 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/dce2209d-5c80-49c6-95e2-c7eb787a26de">
  <img width="1022" alt="Screenshot 2024-06-17 at 1 20 57 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c138af3b-0cdc-4890-aaa1-f4ffe70dc889">
  <img width="1013" alt="Screenshot 2024-06-17 at 3 02 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a28f90d0-b696-4047-be58-9c5a5907f270">
  
      public class SearchInRotatedSortedArray {
      public static void main(String[] args) {

        //Leetcode Medium
        //Very important question

        int[] nums = {3,5,1};
        int target = 3;

        System.out.println(search(nums, target));
      }
      public static int search(int[] nums, int target) {

        int size = nums.length;
        int pivot = pivot(nums);

        System.out.println("Pivot: " + pivot);

        if(pivot == -1){
            //array is not rotated, do normal binary search
            return binarySearch(nums,0,size-1, target);
        }
        else{
            if(nums[pivot]==target)
                return pivot;
            else if(target>=nums[0])
                return binarySearch(nums, 0, pivot-1, target);
            else
                return binarySearch(nums, pivot+1, size-1, target);
        }
       }

       public static int pivot(int[] nums){
        int start = 0;
        int end = nums.length-1;
        int mid=-1;

        while(start<=end){
            mid = start + (end-start)/2;

            if(mid<end && nums[mid+1]<nums[mid])
                return mid;
            if(mid>start && nums[mid-1]>nums[mid])
                return mid-1;
            if(nums[start]>=nums[mid])
                end=mid-1;
            else
                start=mid+1;
        }

        return -1;
      }

      public static int binarySearch(int[] nums, int start, int end, int target){

        while(start<=end){
            int mid = start + (end-start)/2;

            if(target<nums[mid])
                end=mid-1;
            else if(target>nums[mid])
                start=mid+1;
            else
                return mid;
        }

        return -1;
      }
      }


  ## Q9. **What if the array contains duplicate values?** <a name="question9"></a>
  
  <img width="1013" alt="Screenshot 2024-06-17 at 3 02 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a28f90d0-b696-4047-be58-9c5a5907f270">
  <img width="1009" alt="Screenshot 2024-06-17 at 3 03 08 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e0e0edbe-c92a-48d8-8812-e7cc41ec641e">
  <img width="1011" alt="Screenshot 2024-06-17 at 3 03 19 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/33a03af2-fda2-41ac-bb3c-25b37f7440dd">
  <img width="1011" alt="Screenshot 2024-06-17 at 3 03 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0c58c667-0ea1-4757-b295-6db4798e11be">
  <img width="1012" alt="Screenshot 2024-06-17 at 3 03 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/377854c7-8e74-4b38-9395-e23a2d11d548">
  <img width="1018" alt="Screenshot 2024-06-17 at 3 03 50 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/13cb7010-0f0b-45b1-9bd6-a7ea311113da">
  <img width="1022" alt="Screenshot 2024-06-17 at 3 04 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/089ecfaf-21ba-496d-bed5-c38cd7119942">
  <img width="1018" alt="Screenshot 2024-06-17 at 3 04 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3ccc05d2-3834-4719-b2c5-07903b88e7ab">
  <img width="1023" alt="Screenshot 2024-06-17 at 3 04 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0a5fd5e5-3166-4c08-b4d2-c7efdb29eff9">

      static int findPivotWithDuplicates(int[] arr) {
        int start = 0;
        int end = arr.length - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            // 4 cases over here
            if (mid < end && arr[mid] > arr[mid + 1]) {
                return mid;
            }
            if (mid > start && arr[mid] < arr[mid - 1]) {
                return mid-1;
            }

            // if elements at middle, start, end are equal then just skip the duplicates
            if (arr[mid] == arr[start] && arr[mid] == arr[end]) {
                // skip the duplicates
                // NOTE: what if these elements at start and end were the pivot??
                // check if start is pivot
                if (start < end && arr[start] > arr[start + 1]) {
                    return start;
                }
                start++;

                // check whether end is pivot
                if (end > start && arr[end] < arr[end - 1]) {
                    return end - 1;
                }
                end--;
            }
            // left side is sorted, so pivot should be in right
            else if(arr[start] < arr[mid] || (arr[start] == arr[mid] && arr[mid] > arr[end])) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        return -1;
      }



        

  


  


