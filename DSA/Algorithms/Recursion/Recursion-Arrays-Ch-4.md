### Q1. Given an array, find out if it's sorted or not

<img width="969" alt="Screenshot 2024-08-06 at 9 31 30 PM" src="https://github.com/user-attachments/assets/ee0338e5-ffea-40ce-826d-d8d0e57da902">

### Q2. Linear Search

<img width="1007" alt="Screenshot 2024-08-07 at 12 41 58 PM" src="https://github.com/user-attachments/assets/42c6e878-ae13-4601-81ee-ddf4683fd55d">

### Q3. Linear Search (on multiple occurrences)

- #### Return an ArrayList

  <img width="1014" alt="Screenshot 2024-08-07 at 12 43 31 PM" src="https://github.com/user-attachments/assets/d8024b1b-8dac-4c74-8e4f-10f4ed8b2e66">

- #### Return the list without passing the argument

  Challenge: Won't a list be created every time the function is called?

  Yes. However, when the calls return, we can check if their list(list associated with the previous call) has any items. If yes, we can add 
  those to the list associated with the returned function. So, as the stack calls return, it keeps on returning the list items.

  <img width="1019" alt="Screenshot 2024-08-07 at 12 48 16 PM" src="https://github.com/user-attachments/assets/385e845e-56e2-4b49-a471-8d47b5d53f51">
  <img width="1021" alt="Screenshot 2024-08-07 at 12 48 34 PM" src="https://github.com/user-attachments/assets/c4123ae3-040a-4fe7-ae54-91f22d30c861">
  <img width="1023" alt="Screenshot 2024-08-07 at 12 48 47 PM" src="https://github.com/user-attachments/assets/9b04b12c-b1b7-4559-ae62-6568e78bfb79">
  <img width="1024" alt="Screenshot 2024-08-07 at 12 48 56 PM" src="https://github.com/user-attachments/assets/662e09a4-ea88-4d09-ab43-1f0f36102c5c">

  (This is not recommended to use as multiple such lists are created due to which we might face memory issues. However, in some cases, it
  is required to use in this way.)
  
  <img width="1041" alt="Screenshot 2024-08-07 at 11 54 59 AM" src="https://github.com/user-attachments/assets/e2c6c224-1693-492b-b035-ca0aae7f860c">

  We can simplify it even further.

  <img width="1007" alt="Screenshot 2024-08-07 at 11 56 14 AM" src="https://github.com/user-attachments/assets/40d17ee1-a976-487b-943f-44b353971fba">

### Q4. Rotated Binary Search

Consider this array, {4,5,6,7,0,1,2,3}
There are multiple cases that we need to consider. Initially, we can find the "mid".

Case 1: If element in the first index is less than element present at mid, this means the array is sorted in the first half. Now, if target 
        element lies in this section, we can do 

        end = mid-1;

Case 2: Target element is greater than mid, we can do

        start = mid + 1; 
        
Case 2 has two sub-cases.

- If (target<element at mid) & (element at end<element at mid), check if target==start. (If the target element is 7 in the array given)
- If (target<element at mid), check at the right side. We can do,

        start = mid + 1;

<img width="987" alt="Screenshot 2024-08-07 at 12 43 17 PM" src="https://github.com/user-attachments/assets/84aa0abb-4c19-4aeb-aecf-88c425bfc129">

To understand more, check these,

<img width="1019" alt="Screenshot 2024-08-07 at 12 49 40 PM" src="https://github.com/user-attachments/assets/ea3abe8a-d11c-4861-a06b-972139c633f2">
<img width="1023" alt="Screenshot 2024-08-07 at 12 49 46 PM" src="https://github.com/user-attachments/assets/27fe373c-aef7-4391-a035-b38e6f0beb1a">
