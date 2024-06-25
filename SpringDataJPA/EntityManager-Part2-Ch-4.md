## It is not required to create EntityManager on our own. 

##### Why so?

This is because with our current setup/approach, we cannot Autowire EntityManager.

(It is possible but on special cases. In such cases, we are required to use *SpringDataJpa*).

But then if we don't, how will it create the Bean?

##### How to inject EntityManager object then?

    An EntityManager instance is associated with a persistence context. To initialize it, we need to use a special annotation named *@PersistenceContext*.
    A persistence context is a set of entity instances in which for any persistent entity identity, there is a unique entity instance. 
    Within the persistence context, the entity instances and their lifecycle are managed.

    Persistence Context is a place which contains different Entities. It takes the responsibility of persisting entities onto the Database.
   
<img width="1005" alt="Screenshot 2024-06-25 at 8 57 05 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/d53af30e-d750-4608-a299-9600c4ae0a94">

Let's try to run the Application now.

#### Error
   
<img width="975" alt="Screenshot 2024-06-25 at 8 58 27 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/51a305ff-73e8-4f38-8559-8c16df89af9b">

Currently the PersistenceUnit Name is set to "default. Let's first change the Persistence Unit name.

<img width="961" alt="Screenshot 2024-06-25 at 9 00 59 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8b1d4c23-a18d-4f4e-9ff4-d32ef14e40d8">
<img width="927" alt="Screenshot 2024-06-25 at 9 02 24 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/47c00a76-a8b9-48c3-9a20-e648fd48380b">

Run the application and notice unit name in the error.

<img width="539" alt="Screenshot 2024-06-25 at 9 29 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/5dcfce7d-5f7f-4f09-a4a0-366b416c2aee">

Let's now look at the main error.

<img width="973" alt="Screenshot 2024-06-25 at 9 32 30 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/fed854e9-c4f1-410f-b832-62ea8b5d046c">
<img width="687" alt="Screenshot 2024-06-25 at 9 32 44 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7b63cc1b-d617-4261-ad93-392aacfc35f7">


