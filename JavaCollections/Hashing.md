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

### Implementation

- HashMap is internally used as an array of LinkedLists. The indexes are generally refereed as bucket.
  1)n(nodes): Total number of elements
  2)N(size): Total number of buckets(size of the array)
  **How does it know wwhich bucket to add the elements?**
  Through Hashing which essentially changes form of the input. There are multiple techniques like sha1, sha256 etc. It is mostly used for storing passwords.
  - abc->123 (Example)
    
  <img width="560" alt="Screenshot 2024-05-05 at 1 36 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/49070860-089f-45a4-b25e-c0f9912746ab">
  
  ReHashing is done when value of lambda(i.e. n/N) becomes greater than K(threshold value). Now, for lambda<=K we need to increase N(i.e. number of buckets).
  
  <img width="625" alt="Screenshot 2024-05-05 at 1 42 55 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/416fa776-59f0-45ed-b086-b00e9fc59334">
  
  An array of greater size than the previous one is declared and all the elements are moved to the new array. The key of the element is fed to the hash function
  which returns an index/bucket value. The element is then placed to the bucket number obtained.
  
  <img width="854" alt="Screenshot 2024-05-05 at 1 48 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/641b57dd-6b65-4748-885f-82de3d363e5b">
  <img width="1144" alt="Screenshot 2024-05-05 at 1 19 11 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ff3fda7a-1c75-4fa6-84d5-20b01e040ca3">
  <img width="1147" alt="Screenshot 2024-05-05 at 1 23 04 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b55f205c-c746-4f89-b03d-960aee139f36" 
