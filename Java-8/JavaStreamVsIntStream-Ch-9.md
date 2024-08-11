# Boxing - Unboxing & AutoBoxing - AutoUnBoxing

Let's see an example of Bonxing. 

## Boxing & AutoBoxing

For every primitive value, we have a Wrapper class. Boxing is converting primitive type value to respective Wrapper class type done by 
ourselves.

<img width="682" alt="Screenshot 2024-08-11 at 9 58 27 PM" src="https://github.com/user-attachments/assets/2389ce2d-5cd9-4ec2-81d0-7cc777741d3e">

If we don't want to do it ourselves, then it's called autoboxing. Conversion happens internally by the compiler. The compiler does the same as 
what we did earlier.

<img width="672" alt="Screenshot 2024-08-11 at 9 59 08 PM" src="https://github.com/user-attachments/assets/4d811926-d910-4d1d-b271-006eb570e438">

Another example,

<img width="687" alt="Screenshot 2024-08-11 at 10 01 11 PM" src="https://github.com/user-attachments/assets/90a5408e-107b-48e4-9c68-d30893856c70">

## Unboxing & AutoUnboxing

### UnBoxing: Conversion from Wrapper object type to primitive type

#### Example:

<img width="653" alt="Screenshot 2024-08-11 at 10 04 21 PM" src="https://github.com/user-attachments/assets/6a269119-04c6-445d-9b96-6954cde5429a">

### AutoUnboxing: Done automatically by the compiler.

#### Example:

<img width="646" alt="Screenshot 2024-08-11 at 10 02 26 PM" src="https://github.com/user-attachments/assets/86d581d9-2051-493f-a9f3-13954487261a">

We can also write,

<img width="650" alt="Screenshot 2024-08-11 at 10 02 38 PM" src="https://github.com/user-attachments/assets/694a7e5d-a38e-4aa1-8780-e6feca191f9b">

Conversion will happen automatically by the compiler.

Another example,

<img width="651" alt="Screenshot 2024-08-11 at 10 04 07 PM" src="https://github.com/user-attachments/assets/6c8d1728-e97f-4da8-8f4c-a29192fc618f">

## IntStream Interface

"*Stream.of*" is expected to take a bunch of objects. But even if we pass primitives, it is handled by the compiler internally.

<img width="719" alt="Screenshot 2024-08-11 at 10 07 44 PM" src="https://github.com/user-attachments/assets/5465aa9f-7590-47dc-a98d-c66614acdfda">
<img width="959" alt="Screenshot 2024-08-11 at 10 08 26 PM" src="https://github.com/user-attachments/assets/6d363304-5f63-475a-b40f-971e4ad1b3d7">

When we write something like this, there's always overhead that gets associated with the compiler and thus it might have performance issues. 
To work with integers specifically, we have "*IntStream*". This interface is like Stream API interface. It is still a stream but it's
specifically designed to handle primitive **int** type.

Earlier, when we used "*Stream.of*", and then did "*println*", it called the one that takes object in the parameter.

<img width="930" alt="Screenshot 2024-08-11 at 10 11 51 PM" src="https://github.com/user-attachments/assets/d5832aac-ef70-4582-953f-a47a68c853f9">
<img width="654" alt="Screenshot 2024-08-11 at 10 11 59 PM" src="https://github.com/user-attachments/assets/21dea11a-7056-47fb-95fd-20dafe3264ea">

But when we use "*IntStream.of*", that "*println*" method is called whose parameter is int.

<img width="884" alt="Screenshot 2024-08-11 at 10 11 02 PM" src="https://github.com/user-attachments/assets/e15a85b3-65da-4552-b4db-baf348547132">
<img width="643" alt="Screenshot 2024-08-11 at 10 11 17 PM" src="https://github.com/user-attachments/assets/d44001ac-1d7e-44b0-ba2a-e72f5f5fdbdd">
















              
