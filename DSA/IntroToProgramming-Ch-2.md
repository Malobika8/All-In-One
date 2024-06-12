# Types of Languages

<img width="1065" alt="Screenshot 2024-06-12 at 10 30 09 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ff56f55c-5ed7-44e9-9d99-93b44a674123">
<img width="747" alt="Screenshot 2024-06-12 at 10 30 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0bec5917-b230-4e55-ad49-8709a8911248">
<img width="1036" alt="Screenshot 2024-06-12 at 10 57 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bc080c5f-e8b8-4869-ae26-b6060f07e802">

# Memory Management

There are 2 types of memories
* Stack:
  - The variables are stored in stack. The variable would be pointing to the actual value in heap memory
* Heap:
  - Actual values/objects are stored in heap

<img width="784" alt="Screenshot 2024-06-12 at 11 07 58 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/8a7f327a-374a-444a-aaa7-e913e6a17598">

*Note:*
- More than 1 reference variables can point to the same object
- If the object is changed by one reference variable, the change would also be visible to all the other reference variable that are pointing to
  the same object

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Q. What happens when there is no reference variable to an object?

It is removed from memory by Garbage Collector.
