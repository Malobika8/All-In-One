# Binary Search

Binary search is an efficient search algorithm used to find a specific element or value within a sorted list or array. It works by repeatedly
dividing the search interval in half until the target value is found or the search interval is empty. Binary search typically takes O(log n)
time to complete, making it faster than linear search for larger lists. 

<img width="1143" alt="Screenshot 2024-06-14 at 11 31 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3a494fd6-0e7f-443e-9f51-d1944a64d1a1">

## Why Binary Search

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion
of the list that could contain the item, until you've narrowed down the possible locations to just one.

- Best Case: When the target is middle element in the array
  
  <img width="933" alt="Screenshot 2024-06-14 at 11 47 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7e2b1260-0bdf-4eeb-b4b0-eee8c512c4ec">

- Worst Case:

  <img width="1000" alt="Screenshot 2024-06-14 at 11 47 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/cfbd17f2-063f-40b3-80e0-92bbd9a9af2d">
  <img width="1000" alt="Screenshot 2024-06-14 at 11 47 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b39f252a-a7cb-4710-9dca-33c6437cd4fc">
  <img width="994" alt="Screenshot 2024-06-14 at 11 48 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/daa1c7a9-98f0-41e9-ba77-f1537c635d82">
  <img width="1000" alt="Screenshot 2024-06-14 at 11 48 28 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/724c2af3-61ff-40a7-9a5d-2667070b5859">

## Better way to find mid

<img width="1014" alt="Screenshot 2024-06-14 at 11 53 34 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6a9a7c5d-73d0-400b-b83b-f98e6447922e">

## Code for Binary Search (elements sorted in ascending order)

    public class BinaryS {
    public static void main(String[] args) {
        int arr[] = {2,5,7,8,9,12,16,23,27,46};
        int target=23;
        int result = binary(arr,target);
        System.out.println(result);
    }

    public static int binary(int[] arr, int target){
        int start=0;
        int end=arr.length-1;

        while(start<=end){
            int mid=start + (end-start)/2;

            if(target<arr[mid])
                end=mid-1;
            else if(target>arr[mid])
                start=mid+1;
            else
                return mid;
        }

        return -1;
    }
    }

## Order Agnostic Binary Search

Order Agnostic Binary Search says we are given a sorted array but we don't know whether its ascending or descending. The algorithm should
work nonetheless.

An agnostic binary search is a variation of the standard binary search algorithm that is used to search a sorted array of elements for a 
target value. In an agnostic binary search, the algorithm is designed to work for both sorted and unsorted arrays. If the array is sorted,
the algorithm uses binary search to find the target value. If the array is unsorted, the algorithm uses linear search to find the target 
value. This approach can improve the search time in unsorted arrays by avoiding unnecessary comparisons.  

**Approach:** If we are given a sorted array, best way is to compare and check first and last number to determine sorted order.

<img width="1063" alt="Screenshot 2024-06-15 at 12 23 40 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e73ee3a2-7f30-4ad6-9224-e07172691058">

## Code for Order Agnostic Binary Search

    public class OrderAgnosticBinarySearch {
    public static void main(String[] args) {
        int[] arr = {2,4,6,9,11,14,16,19};
        int[] nums = {20,17,16,13,3,2,2,1};
        int target = 9;
        int result = orderAgnosticBinarySearch(arr,target);

        System.out.println(result);
    }
    public static int orderAgnosticBinarySearch(int[] arr, int target){

        int start = 0;
        int end = arr.length-1;
        boolean asc = arr[start]<arr[end];

        while(start<=end){
            int mid = start + (end-start)/2;

            if(target==arr[mid])
                return  mid;

            if(asc){
                if(target<arr[mid]){
                    end=mid-1;
                }
                else{
                    start=mid+1;
                }
            }
            else{
                if(target>arr[mid]){
                    end=mid-1;
                }
                else{
                    start=mid+1;
                }
            }
        }

        return -1;
    }
    }

## Notes

https://github.com/Malobika8/DSA-Bootcamp-Java/tree/main/lectures/10-binary%20search
