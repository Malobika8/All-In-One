# Linear Search

Linear search is a simple search algorithm that works by iterating through an array or list from the beginning to the end until the desired 
element is found or it reaches the end of the list without finding it.

<img width="1076" alt="Screenshot 2024-06-14 at 2 40 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/44d23e2e-4ff3-4cac-9262-fb9f02cd28f2">
<img width="1016" alt="Screenshot 2024-06-14 at 2 39 48 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/de133307-112b-4421-ad54-bf41ce1f90bf">
<img width="1022" alt="Screenshot 2024-06-14 at 2 41 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5dabafc6-56c5-480b-a332-55327725b742">
<img width="936" alt="Screenshot 2024-06-14 at 2 42 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/29349224-b5a8-4511-bddd-75cdefaa40b0">
<img width="840" alt="Screenshot 2024-06-14 at 2 43 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/edc512c8-a9b4-45b3-ab1f-305090dc9132">
![Screenshot 2024-06-14 at 2 45 00 PM](https://github.com/Malobika8/All-In-One/assets/111234135/10afb5aa-f9c4-4e13-b909-0c9a15b1975b)

Here is an example of linear search in Java:

    public static int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
    }

This function takes an integer array arr and an integer target as input, and returns the index of the first occur.



## Notes

https://github.com/Malobika8/DSA-Bootcamp-Java/tree/main/lectures/09-linear%20search
