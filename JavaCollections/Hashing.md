# HashSet

- Set is a collection of unique elements.
- It doesn't preserve the insertion order (Unordered).
- It is an important data structure because of its time complexity ( Insert/Add-O(1) , Search/Contains-O(1) , Delete/Remove-O(1) ).
- Iterator is a variable or symbol that iterates.
- Since set does not have any index, iterator is made use of.

# HashMap
- Map is a collection of key and value pair.
- Map itself is an interface.
- It has unique keys.
- It doesn't preserve the insertion order (Unordered).

## Implementation

- HashMap is internally used as an array of LinkedLists. Initially its a bucket of size 16. The indices are calculated using hashCode & are    generally referred as bucket indices.
  
  1. n(nodes): Total number of elements
  2. N(size): Total number of buckets(size of the array)

   -----------  
  <img width="557" alt="Screenshot 2024-06-27 at 8 40 57 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5a54a6f9-5169-44cc-8c36-ab96d034c9e1">
  <img width="651" alt="Screenshot 2024-06-27 at 8 41 08 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e70c4fbf-3f0b-47d1-aca4-5d8b3dd497cf">
  
  -----------   
  ### How does it know which bucket to add the elements?
  
  Through Hashing which essentially changes form of the input. There are multiple techniques like sha1, sha256 etc. It is mostly used for      storing passwords.
  - abc->123 (Example)
    
  <img width="560" alt="Screenshot 2024-05-05 at 1 36 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/49070860-089f-45a4-b25e-c0f9912746ab">
  
  ReHashing is done when value of lambda(i.e. n/N) becomes greater than K(threshold value). Now, for lambda<=K we need to increase N(i.e. number of buckets).
  
  <img width="625" alt="Screenshot 2024-05-05 at 1 42 55 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/416fa776-59f0-45ed-b086-b00e9fc59334">
  
  An array of double the size than the previous one is declared and all the elements are moved to the new array. The key of the element is  
  fed to the Hash function which returns a bucket index value. The element is then placed to the bucket number obtained.
  
  <img width="854" alt="Screenshot 2024-05-05 at 1 48 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/641b57dd-6b65-4748-885f-82de3d363e5b">
  <img width="1144" alt="Screenshot 2024-05-05 at 1 19 11 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ff3fda7a-1c75-4fa6-84d5-20b01e040ca3">
  <img width="1147" alt="Screenshot 2024-05-05 at 1 23 04 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b55f205c-c746-4f89-b03d-960aee139f36" 

  -----------  
  When we do put and insert a single value, we can see it getting stored in a table.

  <img width="632" alt="Screenshot 2024-06-27 at 8 41 53 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9db11670-67f4-4971-ad35-c8773d76ca77">

  -----------  
  We can see 4 things present

  - hash
  - key
  - value
  - next(this stores address of next node if it exists in case of Has collision)

  <img width="669" alt="Screenshot 2024-06-27 at 8 43 00 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a8aa920a-c2c5-40dd-9d42-2d5625bd5d6f">

  ### Example of Hash Collision.

  We can see "next" stores the address of next node.

  <img width="647" alt="Screenshot 2024-06-27 at 8 43 51 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fa3c790c-40f2-48ac-9e45-97c667e025b6">

  If we expand, we can see the content of next node. Notice that next points to null here since no further nodes exist.

  <img width="658" alt="Screenshot 2024-06-27 at 8 44 14 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/18ba4eb0-1bff-419a-8520-55093b6bc395">

  ### HashMap during duplicate key

  Initially, first key value pair is inserted into the table. However, when we try to put another value, in case the key is duplicate, the     latest value replaces the older value in the table.

  ### HashMap during null key

  If the key is null, it is always inserted to the 0th Bucket.
  
  <img width="817" alt="Screenshot 2024-06-27 at 8 57 11 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8178dfde-6935-414d-b197-acd09159a95c">
  <img width="615" alt="Screenshot 2024-06-27 at 8 57 39 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3d42be0d-bf50-4420-83fe-511d57993386">

  ### Other properties

  <img width="602" alt="Screenshot 2024-06-27 at 8 59 55 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c4e62b28-95e5-4771-91b5-0ed92c0e6f9f">

  - loadFactor: This value indicates that the Map is somewhat full. When this happens, the table is doubled
  - threshold: When map reaches a certain index, table requires to be doubled

  Let's put 13 values to a map.

  <img width="908" alt="Screenshot 2024-06-27 at 9 05 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d99ff8ac-0986-40a3-971a-f5df22cd682a">

  We can see threshold value is 12. So, once 13 elements are inserted the table is doubled.
  
  <img width="606" alt="Screenshot 2024-06-27 at 9 07 15 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c749b2f5-1800-4af8-bad7-12ab0b99f4fd">
  <img width="643" alt="Screenshot 2024-06-27 at 9 09 20 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e7fedd58-a04e-49bf-9473-b68e0960ed19">
  <img width="972" alt="Screenshot 2024-06-27 at 9 09 34 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/566ea804-ee8f-47b6-8fc6-3d641047734f">

  ## FYI

  We usually create HashMap with a default constructor for which default table size is 16.

  ```
  Map<String, Integer> map = new HashMap<>();
  ```

  We can also create a HashMap with initial capacity.

  <img width="552" alt="Screenshot 2024-06-27 at 9 11 59 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f5c5ef3a-c07c-484c-9464-84286c61d286">

  ## Good to Know info

  We can debug Collections effectively using "Show logical structure" option provided by Eclipse.

  1. Example:
 
     <img width="895" alt="Screenshot 2024-06-27 at 9 16 31 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7c755ea9-f72b-46ca-b94b-c85245a8e72a">
     <img width="1110" alt="Screenshot 2024-06-27 at 9 16 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9273d451-9ec6-4832-b0f2-16794a2a604d">
     <img width="1113" alt="Screenshot 2024-06-27 at 9 18 28 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/61b51d95-ec45-46f6-8150-a9623f677f18">
     <img width="557" alt="Screenshot 2024-06-27 at 9 18 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/6cbc175c-4539-4e60-8f94-56b0845052ee">
     <img width="563" alt="Screenshot 2024-06-27 at 9 19 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ad6cbaeb-71fa-4b03-ae4e-7b54db36e557">
     <img width="558" alt="Screenshot 2024-06-27 at 9 19 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f824b22d-4847-4cbd-8f9b-e659e12b17d6">

  2. Example:
 
     <img width="821" alt="Screenshot 2024-06-27 at 9 21 58 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/771a4563-98dd-4311-a8ab-d34605cfb8cc">
     <img width="788" alt="Screenshot 2024-06-27 at 9 22 52 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f56fb887-3653-4956-8f49-4b73ee39d7ca">
     <img width="1101" alt="Screenshot 2024-06-27 at 9 23 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1e6b100e-5205-49f6-b066-736a27dbd4a0">
     <img width="555" alt="Screenshot 2024-06-27 at 9 23 54 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ed411681-549b-4527-a2da-5ffdce2720b0">
     <img width="565" alt="Screenshot 2024-06-27 at 9 24 13 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8e3e96fc-b0a3-4e15-ab05-72895249903d">
     <img width="557" alt="Screenshot 2024-06-27 at 9 24 24 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2c7968d0-ba84-42a6-9a49-a044e43e25de">

  3. Example

     <img width="537" alt="Screenshot 2024-06-27 at 9 26 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/20a83fe2-a5a7-49c3-b860-a4585ad47f44">
     <img width="556" alt="Screenshot 2024-06-27 at 9 26 32 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d8f20ded-0baa-4313-9e43-fe187fefc1ad">
     <img width="543" alt="Screenshot 2024-06-27 at 9 26 50 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b8dee6f4-53ee-4927-9d5a-9e69baaa4c3f">









  
  
