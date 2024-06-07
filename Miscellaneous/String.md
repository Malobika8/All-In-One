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

#### Q. What happends when we try to create String object with same content twice (by using new keyword or double quotes?

   Before creating an object in SCP, it checks if there's any already existing that has the same content. String Constant Pool doesn't allow duplicate objects. Object will be created in
   heap memory though. Heap doesn't have any restriction.
