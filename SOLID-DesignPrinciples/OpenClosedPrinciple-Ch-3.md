# Open Closed Principle

Every software Component should be open for extension but closed for modification. Every Class that we write should be extendable. The change to an 
existing Class should be limited or zero.

Consider a Course class.

<img width="620" alt="Screenshot 2024-07-03 at 8 10 21 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/613b4177-b6c0-4f0b-a80b-f26b634130ca">
<img width="1112" alt="Screenshot 2024-07-03 at 8 11 44 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c7068573-5d8a-44c2-9743-0847258a9edc">

Existing Course class has Java and Spring courses. Suppose we want to add a new course now. 

Should we add Hibernate course to the existing class? In that case, we might need to change multiple times in future for new courses. Rather than
this, we can create Course specific classes for proper seggregation.

<img width="556" alt="Screenshot 2024-07-03 at 8 14 38 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/68caead7-78d9-43c2-bb1b-79862e81ffa5">
<img width="806" alt="Screenshot 2024-07-03 at 8 16 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/3e8b34d4-b333-4555-b7e4-31563cd77ba8">
<img width="812" alt="Screenshot 2024-07-03 at 8 16 30 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/35819520-96cf-410f-a167-0861c4fa7858">
<img width="859" alt="Screenshot 2024-07-03 at 8 16 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ea419065-775e-4c1a-bd22-3bc2236b40e9">

We can have a Helper method (overloaded) that can help in printing Course content.

<img width="925" alt="Screenshot 2024-07-03 at 8 18 27 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2577bcec-82c6-4403-9b31-211e74170661">
<img width="920" alt="Screenshot 2024-07-03 at 8 19 10 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7a02c910-5590-4422-9a48-d6fcf38ddc01">

## Let's try to analyze what issues we might face while adding a new course in future

Suppose we add a new course on Microservices. We would need to add a new Class for the same and overload the print method in Course. This would 
again break the principle.

<img width="859" alt="Screenshot 2024-07-03 at 8 22 21 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8a67c3af-42bd-49ef-9d62-646ed0136455">
<img width="887" alt="Screenshot 2024-07-03 at 8 22 49 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/176e86b0-20ea-4b37-8fcb-f7bca9b805e5">

Rather than that, we can have a Course Interface which can have a print method. All other Courses can implement it and hence have their own print implementation
based on the Course.



