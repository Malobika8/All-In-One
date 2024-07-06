# subString() method in Java

- We can create a String object using double quotes( String name = "XYZ") or by using *new* keyword ( String name = new String("xyz").
- Objects are stored in heap memory in Java
- String internally uses an array of Characters.

Whenever we want some part of a String, we can use the *subString()* method.

Example:

<img width="1126" alt="Screenshot 2024-07-06 at 2 32 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b949bf2c-920f-4b96-8ff8-e285d4e8bb51">

*subString()* creates a new String as **String is immutable**.

```
The substring() function in Java is used to extract a part of a given string. The function returns a new string containing a portion of the
original string, starting from the specified index to the end or to the specified end index.
```

-------------------------

We have another *subString()* method in Java.

*String subString(beginIndex, endIndex)*

Similar to the previous one, it returns a new String that is a substring of the current String.

#### Note: beginIndex is inclusive & endIndex is exclusive

<img width="1117" alt="Screenshot 2024-07-06 at 2 43 17 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/11492d01-bbb3-48c9-99fc-e287a9428e8f">

#### How Java calculates length of a substring?

- *endIndex - beginIndex*

<img width="1120" alt="Screenshot 2024-07-06 at 2 47 21 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/0473142b-c0ba-4fb5-9099-dcaa89a423db">

#### Things to keep in mind while working with *subString()* method

- If we pass a -ve index, we will get an exception.
- If *index>StringLength*, it will through StringIndexOutOfBoundException
- beginIndex cannot be greater than endIndex
- If we pass length of the String in *subString()* method, we will get an empty String

<img width="1114" alt="Screenshot 2024-07-06 at 2 51 31 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a1fdda72-e1e7-4cd4-94e5-bb7709ecf2db">

# How subString() works internally?

In Java 6, with *subString()* method, we had memory leak issue. It was fixed in Java 7/8.

let's observe few things with JDK 1.6.

Consider the following piece of code,

<img width="807" alt="Screenshot 2024-07-06 at 2 58 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/31e6df55-a792-4d19-9288-edebc44de57d">

If we debug, we can see value of "str"

<img width="918" alt="Screenshot 2024-07-06 at 2 59 33 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e6e6d289-ade4-4116-82a0-fac4f8dee027">
<img width="1111" alt="Screenshot 2024-07-06 at 3 00 00 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/943ff338-c003-447e-b895-bfcb9f6565cd">

Now, since "str1" holds a part of the String "str", it should ideally contain only two characters "am".

<img width="914" alt="Screenshot 2024-07-06 at 3 00 40 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/583186ad-c015-4104-a631-8da76fac1fa7">

But if we expand, we will see it still points to the value of original String "str"

<img width="1110" alt="Screenshot 2024-07-06 at 3 01 13 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7e1d2d6e-c50b-4b67-93c0-f0e6e6970e0f">

So, although value of "str" is not used anymore, it can't be freed by the Garbage Collector as it is still referenced by "str1".

This leads to *Memory Leak* in Java 6.

#### How are we still getting the correct value then? i.e. "am"

This is because of count and offset. It starts from offset 6 and counts 2 characters.

<img width="1077" alt="Screenshot 2024-07-06 at 3 06 14 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8935b079-108f-4c60-897d-3e3ecb93cb16">

### Let's try to understand why this problem occurred in the first place

<img width="1068" alt="Screenshot 2024-07-06 at 3 08 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/90d408ed-32c6-4c6c-bd48-c2981717b774">

Check the last condition,

<img width="1002" alt="Screenshot 2024-07-06 at 3 08 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e9c76aac-666b-419a-92bc-ac053a0ea2b0">

<img width="1150" alt="Screenshot 2024-07-06 at 3 09 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/52e94120-5115-4a19-ba21-cb3c53f2ed46">

*value* is nothing but the original char array which is what was being sent. This caused Memory Leak as it returned back the original char array
but with different offset and count value.

<img width="952" alt="Screenshot 2024-07-06 at 3 09 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5db48168-315f-45b6-ac0c-966139f2000b">

If we go to the String constructor we would notice that the value set is the original char array. Although offset and count is changed, value
is not changed.

<img width="1015" alt="Screenshot 2024-07-06 at 3 11 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/69390f38-d9cb-4537-8c94-9e69c7dc0114">
<img width="1150" alt="Screenshot 2024-07-06 at 3 13 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b6b954ff-e75f-476c-a492-c9f2c0d95f30">

### Let's check now how this was fixed in Java 7

We will use jdk 1.8

Let's run the same program and debug.

<img width="1078" alt="Screenshot 2024-07-06 at 3 14 29 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2ad03f0e-705c-49f9-ace8-0a65ee53fabd">

value of "str"

<img width="1117" alt="Screenshot 2024-07-06 at 3 14 55 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/47998027-0a0e-49dc-b3be-87431668b272">
<img width="1101" alt="Screenshot 2024-07-06 at 3 15 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8688fb9e-247a-4b80-9402-3ba74405ce84">

This time it stores only the part required.

<img width="1113" alt="Screenshot 2024-07-06 at 3 15 56 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a432529e-4a49-465a-80e1-b933bb7e7787">

Also, we would notice that this version doesn't create offset and count.

This time we can notice, it calculates and sets only what is required.

<img width="1084" alt="Screenshot 2024-07-06 at 3 17 02 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/50c98cf4-6594-4cac-b5e7-e96de2b72f56">
<img width="1040" alt="Screenshot 2024-07-06 at 3 20 13 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/1d944e1f-bd6d-463d-924d-ca3ddceac1c2">
<img width="1147" alt="Screenshot 2024-07-06 at 3 21 32 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/047cbb21-e9b7-44b5-bf52-112b8edb5064">

## Memory 

- Java 6: Refers the same array and finds substring using offset and count. Garbage collection wasn't efficient. Led to Memory leak.

  <img width="530" alt="Screenshot 2024-07-06 at 3 27 10 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ff54add2-d37c-46e8-8044-6b804d17bc54">

- Java 7: Creates a new array with required characters

  <img width="528" alt="Screenshot 2024-07-06 at 3 27 58 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2cc4642c-1a63-4448-8f76-02fd9c21143e">



