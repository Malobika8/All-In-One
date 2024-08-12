# Boxing - Unboxing & AutoBoxing - AutoUnBoxing

## 1. Boxing & AutoBoxing

Let's see an example of Boxing. 

For every primitive value, we have a **Wrapper** class. 

```
Boxing is basically converting primitive type value to respective Wrapper class type done by ourselves.
```

<img width="682" alt="Screenshot 2024-08-11 at 9 58 27 PM" src="https://github.com/user-attachments/assets/2389ce2d-5cd9-4ec2-81d0-7cc777741d3e">

If it happens implicitly, it's called "**Autoboxing**". Conversion happens internally by the "Compiler". The compiler does the same as what we did earlier.

<img width="672" alt="Screenshot 2024-08-11 at 9 59 08 PM" src="https://github.com/user-attachments/assets/4d811926-d910-4d1d-b271-006eb570e438">

Another example,

<img width="687" alt="Screenshot 2024-08-11 at 10 01 11 PM" src="https://github.com/user-attachments/assets/90a5408e-107b-48e4-9c68-d30893856c70">

## 2. Unboxing & AutoUnboxing

### UnBoxing: 
Conversion from Wrapper object type to primitive type

#### Example:

<img width="653" alt="Screenshot 2024-08-11 at 10 04 21 PM" src="https://github.com/user-attachments/assets/6a269119-04c6-445d-9b96-6954cde5429a">

### AutoUnboxing: 
Done automatically by the compiler.

#### Example:

<img width="646" alt="Screenshot 2024-08-11 at 10 02 26 PM" src="https://github.com/user-attachments/assets/86d581d9-2051-493f-a9f3-13954487261a">

We can also write,

<img width="650" alt="Screenshot 2024-08-11 at 10 02 38 PM" src="https://github.com/user-attachments/assets/694a7e5d-a38e-4aa1-8780-e6feca191f9b">

Conversion happens automatically by the Compiler.

Another example,

<img width="651" alt="Screenshot 2024-08-11 at 10 04 07 PM" src="https://github.com/user-attachments/assets/6c8d1728-e97f-4da8-8f4c-a29192fc618f">

## IntStream Interface

"*Stream.of*" is expected to take a bunch of objects. But even if we pass primitives, it is handled by the compiler internally.

<img width="719" alt="Screenshot 2024-08-11 at 10 07 44 PM" src="https://github.com/user-attachments/assets/5465aa9f-7590-47dc-a98d-c66614acdfda">
<img width="959" alt="Screenshot 2024-08-11 at 10 08 26 PM" src="https://github.com/user-attachments/assets/6d363304-5f63-475a-b40f-971e4ad1b3d7">

However, implicit conversion has overhead associated with the Compiler and might have performance issues. 

To work with integers specifically, we have "*IntStream*". This interface is similar to Stream API interface. It is still a stream but it's
specifically designed to handle primitive **int** type.

Earlier, when we used "*Stream.of*", and did "*println*", it called the one that takes object in the parameter.

<img width="930" alt="Screenshot 2024-08-11 at 10 11 51 PM" src="https://github.com/user-attachments/assets/d5832aac-ef70-4582-953f-a47a68c853f9">
<img width="654" alt="Screenshot 2024-08-11 at 10 11 59 PM" src="https://github.com/user-attachments/assets/21dea11a-7056-47fb-95fd-20dafe3264ea">

However, when we use "*IntStream.of*", that "*println*" method is called whose parameter is int.

<img width="884" alt="Screenshot 2024-08-11 at 10 11 02 PM" src="https://github.com/user-attachments/assets/e15a85b3-65da-4552-b4db-baf348547132">
<img width="643" alt="Screenshot 2024-08-11 at 10 11 17 PM" src="https://github.com/user-attachments/assets/d44001ac-1d7e-44b0-ba2a-e72f5f5fdbdd">

Whenever we store any primitive value (say int i = 10), it takes 4 bytes of memory. But an object type like Integer takes 20 bytes of memory.

<img width="705" alt="Screenshot 2024-08-12 at 9 53 40 AM" src="https://github.com/user-attachments/assets/2c5cc21d-4da3-4342-94b0-3dba5f944e2b">

Similarly, we have DoubleStream, LongStream, and other such interfaces.

<img width="735" alt="Screenshot 2024-08-12 at 9 54 51 AM" src="https://github.com/user-attachments/assets/ef877d60-79ca-4d5d-8df7-02d92322d047">

### Advantages

- It has multiple utility methods that can be utilized directly.

  <img width="672" alt="Screenshot 2024-08-12 at 9 57 06 AM" src="https://github.com/user-attachments/assets/b9c00e65-61f4-411b-a693-5416353575fd">
  <img width="647" alt="Screenshot 2024-08-12 at 9 57 51 AM" src="https://github.com/user-attachments/assets/1f97ad43-f4f1-427c-8ab0-ebc4a9a829f4">

  ### *reduce* in Stream
  
  #### How to find sum from a Stream of integers?

  There's no in-built method called "*sum*" but we can utilize "*reduce*".

  <img width="1024" alt="Screenshot 2024-08-12 at 10 05 26 AM" src="https://github.com/user-attachments/assets/e93ca1ce-b6f6-4c47-9e4d-88de1521dcfc">

  #### How does reduce work?

  In "*reduce*", we get several elements.

  This is how it works,

  <img width="746" alt="Screenshot 2024-08-12 at 10 08 58 AM" src="https://github.com/user-attachments/assets/66f8299e-c440-48bb-9655-49ab081e2337">

  We can even print it and see,

  <img width="971" alt="Screenshot 2024-08-12 at 10 09 26 AM" src="https://github.com/user-attachments/assets/7bc6fd3b-7912-4278-8f0d-41763aa85a5a">
  <img width="745" alt="Screenshot 2024-08-12 at 10 09 46 AM" src="https://github.com/user-attachments/assets/79e2ac03-da33-4119-ad06-44e620f9a69e">

  We can even do "*peak*" to understand better.

  <img width="1067" alt="Screenshot 2024-08-12 at 10 10 49 AM" src="https://github.com/user-attachments/assets/5fd51fc5-4c91-4525-bb37-f58acca96452">
  <img width="745" alt="Screenshot 2024-08-12 at 10 11 01 AM" src="https://github.com/user-attachments/assets/a1ecdbf9-6559-4c09-9623-70d00178756b">

  Final,

  <img width="976" alt="Screenshot 2024-08-12 at 10 12 19 AM" src="https://github.com/user-attachments/assets/8ff02e11-ade9-41ea-b4fc-0c766c30fbe8">

  We can also reuse "*sum()*" method of Integer class,

  <img width="1016" alt="Screenshot 2024-08-12 at 10 13 22 AM" src="https://github.com/user-attachments/assets/3b9c88c5-98c7-44e4-9239-aab1c434a672">

  OR

  <img width="955" alt="Screenshot 2024-08-12 at 10 13 56 AM" src="https://github.com/user-attachments/assets/83edbfa9-6603-442c-88c3-67c6118d4acc">

  We can even provide the first value as 0.

  <img width="929" alt="Screenshot 2024-08-12 at 10 17 35 AM" src="https://github.com/user-attachments/assets/df2bbab0-a9aa-426c-adaa-80486f883be8">
  <img width="935" alt="Screenshot 2024-08-12 at 10 17 48 AM" src="https://github.com/user-attachments/assets/bdc560ac-e09e-4013-bf43-89513ac21565">
  <img width="922" alt="Screenshot 2024-08-12 at 10 17 56 AM" src="https://github.com/user-attachments/assets/2f2c034c-5d2d-48db-81e8-bb3cfd887be9">
  <img width="953" alt="Screenshot 2024-08-12 at 10 18 10 AM" src="https://github.com/user-attachments/assets/92699020-70ed-4ba5-8eb0-5434e4e87407">
  <img width="968" alt="Screenshot 2024-08-12 at 10 18 35 AM" src="https://github.com/user-attachments/assets/aec0c9d1-dc76-4aee-ba66-fb46902d3ee2">

# Unboxing in Stream API

We can convert Stream of integers to IntStream and let the Compiler do auto unboxing. For this, we can use "*mapToInt*" function available in Stream

<img width="991" alt="Screenshot 2024-08-12 at 10 39 06 AM" src="https://github.com/user-attachments/assets/ce331d64-1890-44fc-b057-5b6e5c458924">

We have a Functional Interface "*ToIntFunc*".

<img width="749" alt="Screenshot 2024-08-12 at 10 39 22 AM" src="https://github.com/user-attachments/assets/a770c1f0-a989-4e5a-93b1-9612dcd2b34c">

We can use these to convert.

<img width="1022" alt="Screenshot 2024-08-12 at 10 40 53 AM" src="https://github.com/user-attachments/assets/4bc446b7-efa9-40dd-8de1-0d56df791673">

We can even do it by ourselves by using "*intValue()*" method that converts from Integer to int.

<img width="960" alt="Screenshot 2024-08-12 at 10 44 12 AM" src="https://github.com/user-attachments/assets/9f82d62c-2117-4c54-a75b-daadd4cca670">

We can reduce it like this,

<img width="951" alt="Screenshot 2024-08-12 at 10 45 50 AM" src="https://github.com/user-attachments/assets/1935a578-caa9-41a5-be0c-790bf4cdecc7">

OR

<img width="966" alt="Screenshot 2024-08-12 at 10 48 40 AM" src="https://github.com/user-attachments/assets/28751ca1-2d97-4d8f-a6f8-52d8b7738c92">

## "*boxed()*" in Stream API

### Convert a set of ints to Integers?

<img width="735" alt="Screenshot 2024-08-12 at 10 53 55 AM" src="https://github.com/user-attachments/assets/f0e44aa1-ef64-4441-86d0-1c0499afcb66">

The last one is exclusive in range.

"*rangeClosed()*" is inclusive.

<img width="721" alt="Screenshot 2024-08-12 at 10 54 21 AM" src="https://github.com/user-attachments/assets/3b1f0497-334f-414a-861f-d28fefb023b5">

*Requirement*: Apply "*hashCode()*" method over every integer passed.

We cannot use "*hashCode*" directly on primitive numbers.

<img width="664" alt="Screenshot 2024-08-12 at 10 57 05 AM" src="https://github.com/user-attachments/assets/b5312006-a19f-48fe-9caf-0edb687778c1">

We need to first convert the numbers to Integer object and then hashCode can be used.

"*boxed()*" does the same for us.

<img width="666" alt="Screenshot 2024-08-12 at 11 00 53 AM" src="https://github.com/user-attachments/assets/fd69d6b3-9668-40cf-a390-f7dd2f307c58">
<img width="666" alt="Screenshot 2024-08-12 at 11 01 15 AM" src="https://github.com/user-attachments/assets/eca6564a-efc2-4d91-8fbd-30e36a89dfb2">

"*boxed()*" returns a Stream of integers. It does **AutoBoxing**.

<img width="666" alt="Screenshot 2024-08-12 at 11 01 15 AM" src="https://github.com/user-attachments/assets/8445fc06-dad4-4087-a360-3757c5d82143">
<img width="870" alt="Screenshot 2024-08-12 at 11 03 02 AM" src="https://github.com/user-attachments/assets/6d11521c-f17a-4113-8a6d-0daef2046948">

# Guess the output

<img width="759" alt="Screenshot 2024-08-12 at 11 16 27 AM" src="https://github.com/user-attachments/assets/d70c5bc1-0ad8-447b-b3a7-434d338546d7">
<img width="826" alt="Screenshot 2024-08-12 at 11 16 34 AM" src="https://github.com/user-attachments/assets/c1e6fed9-3cb0-4683-b80a-9bb6582d91bf">

