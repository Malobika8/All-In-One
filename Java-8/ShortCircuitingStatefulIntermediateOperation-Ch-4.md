----------------------------
Methods mentioned in this doc:
- sorted()
- iterator()
- limit()
- filter()
- takeWhile()
- skip()
- distinct()
----------------------------

## Stateful or Stateless behavior of an Intermediate operation

<img width="1149" alt="Screenshot 2024-07-23 at 8 04 08 PM" src="https://github.com/user-attachments/assets/1556296e-b00e-4113-9e54-9d326ea1f018">

- A stateless operation doesn't need to know about any other element to be able to emit a result. 

  Examples of Stateless operations are: filter(), map() or flatMap()

- When an operation requires retaining the information of the elements it has processed so far to process the current element then it is a 
  stateful operation.

  Example of Stateful operations are: skip(), distinct(),limit() and sorted()

# Stateful Vs Stateless Operation

#### Stateful methods: Retains the State of the element that it tries to process.

### Let's sort an array.

*sorted()* sorts all the data in Natural Order. It's a *Stateful Intermediate Operation*.

<img width="669" alt="Screenshot 2024-07-23 at 8 15 52 PM" src="https://github.com/user-attachments/assets/da040a8a-626c-43eb-b4db-39dc2e7c301b">
<img width="867" alt="Screenshot 2024-07-23 at 8 16 42 PM" src="https://github.com/user-attachments/assets/cdff8bd0-fbe7-45a0-a3a4-6db6270d3281">

*sorted()* method gets all the elements from the Source Stream and then sorts it. It is called Stateful Operation because it has kind of a 
temporary memory where it stores all the elements, sorts them, and later forwards them. 

- *sorted()* doesn't process Data one by one.
- *sorted()* needs to see all the elements before performing the operation.

<img width="1026" alt="Screenshot 2024-07-23 at 8 23 55 PM" src="https://github.com/user-attachments/assets/7d01088a-e8ac-41de-a99a-3226c989e9ee">
<img width="780" alt="Screenshot 2024-07-23 at 8 24 31 PM" src="https://github.com/user-attachments/assets/a4862ccb-df86-4c0e-b009-4065bbdb9844">

<img width="1099" alt="Screenshot 2024-07-23 at 8 29 39 PM" src="https://github.com/user-attachments/assets/a428a9aa-eb20-44b6-85ac-28e003a3fa08">
<img width="1109" alt="Screenshot 2024-07-23 at 8 30 32 PM" src="https://github.com/user-attachments/assets/8eb38496-73b7-41c0-81ad-df365314be25">

<img width="1120" alt="Screenshot 2024-07-23 at 8 31 24 PM" src="https://github.com/user-attachments/assets/c62844a0-0c08-483a-962d-4194b5ed638f">
<img width="1141" alt="Screenshot 2024-07-23 at 8 31 08 PM" src="https://github.com/user-attachments/assets/913e24b1-a8d5-430b-8490-f19ca7c5107e">

### Let's set an Infinite Stream

Consider the *iterator()* method which takes seed and Unary Operator. *iterator()* method returns Infinite Stream.

<img width="776" alt="Screenshot 2024-07-23 at 8 40 28 PM" src="https://github.com/user-attachments/assets/401b5b7d-9f46-4d0f-b7bb-cb0ed03e68b3">
<img width="937" alt="Screenshot 2024-07-23 at 8 41 45 PM" src="https://github.com/user-attachments/assets/21f81b65-ac22-4516-947e-21d03b118728">

<img width="797" alt="Screenshot 2024-07-23 at 8 42 22 PM" src="https://github.com/user-attachments/assets/55e1ec39-cf1b-41db-b0e6-0cfeedf437af">

This keeps on printing the Integers infinitely.

<img width="821" alt="Screenshot 2024-07-23 at 8 43 46 PM" src="https://github.com/user-attachments/assets/1f2402e1-f3b3-413e-ac47-ea14b87d3315">

It will keep on checking for new integers.

However, *limit()* shortcircuits the pipeline and stops the Operation right away once the condition is not satisfied.

<img width="817" alt="Screenshot 2024-07-23 at 8 45 00 PM" src="https://github.com/user-attachments/assets/55aab098-e773-453e-af8e-687e83a426af">

Hence, it is called a Short Circuit Stateful Operation.

<img width="760" alt="Screenshot 2024-07-23 at 8 46 07 PM" src="https://github.com/user-attachments/assets/0a33aace-ba75-4ab6-8b3c-8dc10363c0b0">
<img width="819" alt="Screenshot 2024-07-23 at 8 46 28 PM" src="https://github.com/user-attachments/assets/8cbe5cfc-94b4-47b3-a626-743d97c7ff33">

#### Note: It is not required for *limit()* to take all the inputs first before performing the Operation.

### Q. What happens if we use *sorted()* with an Infinite Stream?

Since it is a *Stateful Operation*, it keeps on waiting for all the elements so that it can operate on all at once. This ultimately leads to
*OutOfMemory* Exception.

<img width="818" alt="Screenshot 2024-07-23 at 8 48 56 PM" src="https://github.com/user-attachments/assets/ac047069-b801-4f04-af65-019c6e8d8dfd">

### Let's look at another Short Circuiting Stateful Intermediate Operation (*takeWhile()*).

Imagine we have a Source Stream and want a "filter" (integers less than 8). Note that *filter()* is a Stateless function.

Let's say we want to find the square of all the elements that satisfy the filter condition.

<img width="798" alt="Screenshot 2024-07-23 at 8 54 58 PM" src="https://github.com/user-attachments/assets/f783bafd-0839-49be-843f-aa5a271d048c">
<img width="1053" alt="Screenshot 2024-07-23 at 8 56 00 PM" src="https://github.com/user-attachments/assets/597abdfb-650d-49d4-8696-257c5862078c">
<img width="806" alt="Screenshot 2024-07-23 at 8 56 29 PM" src="https://github.com/user-attachments/assets/c6514a1c-fab4-4e70-99dc-1b496c3f6071">
<img width="763" alt="Screenshot 2024-07-23 at 8 56 54 PM" src="https://github.com/user-attachments/assets/c18fb15d-34b0-4f48-9489-200493bc77cd">

*takeWhile()* does a similar operation as that of *filter()*. The only difference is the short-circuiting property of *takeWhile()*.

<img width="732" alt="Screenshot 2024-07-23 at 8 58 20 PM" src="https://github.com/user-attachments/assets/20683dfb-d73c-4500-80ca-0b6005a89223">
<img width="773" alt="Screenshot 2024-07-23 at 8 59 37 PM" src="https://github.com/user-attachments/assets/1125a47f-6a18-4c4b-acd7-b4ea21a56130">
<img width="746" alt="Screenshot 2024-07-23 at 8 59 53 PM" src="https://github.com/user-attachments/assets/2d03bdc7-e540-4248-95fc-0b07e583c0b2">
<img width="747" alt="Screenshot 2024-07-23 at 9 00 03 PM" src="https://github.com/user-attachments/assets/9455cbf9-dd95-41c7-b39e-f8fdd0b4c5c5">

#### Note: It is not required for *takeWhile()* to take all the inputs first before performing the Operation.

The moment the condition doesn't match, it short circuits and stops checking further.

Let's see another example. 

<img width="773" alt="Screenshot 2024-07-23 at 9 04 08 PM" src="https://github.com/user-attachments/assets/d11b211e-ab7a-4b21-82e7-76703036d859">

Since the first condition fails, it short circuits and stops the Data flow. Hence, nothing is printed on Console.

<img width="749" alt="Screenshot 2024-07-23 at 9 04 42 PM" src="https://github.com/user-attachments/assets/7129e230-a278-4a91-8214-3c30b35c5f9d">

Example 2:

<img width="818" alt="Screenshot 2024-07-23 at 9 06 16 PM" src="https://github.com/user-attachments/assets/e86d36ae-9ae1-4719-b8cd-c94cd0aaceb8">

### *skip()* & *distinct()*

* skip(): It is again a *Stateful Intermediate Operation*.

  <img width="814" alt="Screenshot 2024-07-23 at 9 17 59 PM" src="https://github.com/user-attachments/assets/a65e8495-6599-46ef-9c50-cb5944f1c453">

  Skip the first 3 elements.

  <img width="803" alt="Screenshot 2024-07-23 at 9 17 10 PM" src="https://github.com/user-attachments/assets/66c631e2-c49a-45c9-9c5b-0c6266c194ec">

* distinct(): it is again a *Stateful intermediate operation*.

  <img width="797" alt="Screenshot 2024-07-23 at 9 19 14 PM" src="https://github.com/user-attachments/assets/d2ee8f86-ad6e-45e5-bed8-61b3516c896f">

  <img width="815" alt="Screenshot 2024-07-23 at 9 20 20 PM" src="https://github.com/user-attachments/assets/507617ac-dbe8-4d70-96ce-7157badf6c48">


