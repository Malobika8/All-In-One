# Strings

* 4 ways to represent String in Java:

  - String (Class in java.lang package)
      - Using new Keyword (Example: String s1 = new String("example");        
      - Using "" (Example: String s1 = "example";
  - StringBuffer
  - StringBuilder
  - Arrays
 
* Where the String object is created in memory?

  The object is created in String Constant Pool first. Since we use new keyword to create an object of String, object is created in heap memory. Whenever String objects are created, it is
  stored in the form of indexes.
  When we create an object using new keyword, it points to object created in heap memory.
  When we create String using double quotes, it creates an object only in String Constant pool.

#### Q. What happens when we try to create String object with same content twice (by using new keyword or double quotes)?

Before creating an object in SCP, it checks if there's any existing String that has the same content. String Constant Pool doesn't allow duplicate objects. Object will be created in
heap memory though. Heap doesn't have any restriction.

## Immutable

#### Q. Why String is immutable in Java?

Immutable class in java means that once an object is created, we cannot change its content. In Java, all the wrapper classes (like           Integer, Boolean, Byte, Short) and String class is immutable.

We know that a String constant is stored in *String Object Pool* & it doesn't allow duplicates. So everytime a new String object is created
with the same content as the one already present in SCP, rather than creating/adding a new constant/object in SCP, it references the one that is already available in SCP. 

<img width="1133" alt="Screenshot 2024-06-07 at 9 08 42 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/768d3f79-2581-4bd4-9328-eaf8e0a8cd3d">

Suppose, an existing String is concatenated with another String and the object in SCP is modified. If Strings were mutable, the references would become invalid as the constant in SCP is modified

** *FYI: * When we create an object of a String using *new* keyword, object is created in Heap memory. However, if the constant is already present in SCP, then rather than getting the String from heap, we can get it from SCP using *intern()* method.

<img width="1069" alt="Screenshot 2024-06-07 at 9 27 35 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/f17a2bb5-9a49-4700-9f1e-bfe50cf79399">
---------------------------------------------
As we have discussed, Strings are immutable which means it's value can't be changed. Now, let's look into the below example to understand why String objects are immutable in Java:

<img width="659" alt="Screenshot 2024-06-07 at 10 53 44 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/27cb266c-7ad0-48c1-8215-920862b58878">

Strings in Java are specified as immutable, as seen above because strings with the same content share storage in a single pool to minimize creating a copy of the same value. That is to say, once a String is generated, its content cannot be changed and hence changing content will lead to the creation of a new String. Otherwise, the update will affect the heap value, and then all other String references that share the same storage location will be changed. This change has the potential to be unpredictable, which is why it is not desirable.

## HashCode Caching

#### Q. Why String is used most as the key of HashMap?

The advatange of String being immutable is that its hashcode could be cached.

Caching the hashcode of an object is very useful in operations where it needs to be calculated frequently. It avoids the recalculation of hashcode again and again and thus increase application performance.

One such operation where hashcode caching is very useful is using an object as a key in maps like HashMap.

Strings are frequently used as keys in maps so it is a best case for caching the hashcode. String class has a built-in hashcode caching mechanism.

According to Java API Docs the hash code for a String object is computed as


     s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]

using int arithmetic, where s[i] is the ith character of the string, n is the length of the string, and ^ indicates exponentiation. (The hash value of the empty string is zero.) 

It shows that hashcode of a String object depends on its contents.

Now for caching the hashcode for an object whose hashcode depends on its contents, it is necessary for that object to be [immutable]. Otherwise when contents of that object would be changed then hashcode also get changed. Thus caching of hashcode of a such mutable object is of no use. Since strings in Java are immutable we can cache its hashcode.

If you look ito the source code of String class, you will find following definition of hashCode() method :

    public int hashCode() {
        int h = hash;
        if (h == 0 && count > 0) {
            int off = offset;
            char val[] = value;
            int len = count;

        for (int i = 0; i < len; i++) {
            h = 31*h + val[off++];
        }
        hash = h;
        }

       return h;
    }

Notice the statement, 

    int h = hash;

Here variable h is assigned to a variable hash. This variable hash is used to store the haschode for a String object. "hash" variable is defined as:

         ** Cache the hash code for the string */
         private int hash; // Default to 0

Hashcode for strings are cached on per object basis i.e each String object's hashcode is stored in this private variable hash.

Whenever hashCode() method of String class is called, the value of variable hash is checked whether it is 0 or not as indiated by line 1495 and 1496. Variable hash equals to 0 means that hashcode() method is being called first time and hashcode has not been calculated yet.

If hash is equals to 0, only then hashcode for correspoding String object is calculated and cached in variable hash as shown in line 1504.

So when the next time hashCode() for the same String object  is called, value of hash does not come out to be 0 and hashcode is not recalcuated but is reused as stored in variable hash.

<img width="1140" alt="Screenshot 2024-06-07 at 10 58 41 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/917d898a-ffa8-4400-b4d5-b52bf481f0c4">
<img width="864" alt="Screenshot 2024-06-07 at 10 59 56 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1c427149-8d55-4a95-bb2b-7789bb4eb294">
<img width="902" alt="Screenshot 2024-06-07 at 11 00 31 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dd9bdb3c-7823-43a7-8260-3da4326fd419">
<img width="977" alt="Screenshot 2024-06-07 at 11 00 59 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/dc0711a8-fc4f-4c47-8c98-3539329cfbfa">
<img width="852" alt="Screenshot 2024-06-07 at 11 02 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9e5c03ff-cedc-4945-9396-47bd9365cbdf">
<img width="1128" alt="Screenshot 2024-06-07 at 11 03 45 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/0eb356c4-7421-4662-aa91-a783fa8c6db5">
<img width="1134" alt="Screenshot 2024-06-07 at 11 05 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3b75473b-1dd5-429b-af8f-d5d8f5ba7c7c">
<img width="1126" alt="Screenshot 2024-06-07 at 11 13 24 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/16e4bd54-1c25-49e3-84b1-9bd5ced2d931">

#### Must Read: 

https://animeshgaitonde.medium.com/the-curious-case-of-java-string-hashcode-6d98c734a313
