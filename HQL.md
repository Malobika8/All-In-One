# **Hibernate Query Language**

Get and load fetches the data based on Id's or primary key. What about complex queries? We would need **HQL(Hibernate Query Language)** in that case.
* SQL: Select * from xyzTable;
* HQL: from xyzTable

<img width="1083" alt="Screenshot 2024-05-08 at 10 31 49 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/c086a6f8-1c6c-4aee-a698-d8b56f07d968">

For dynamic queries, a parameter can be passed and set using session's setParameter method.

<img width="1044" alt="Screenshot 2024-05-08 at 11 08 45 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/44e05be2-7b7f-4cb6-ab93-2df58757fc9f">
<img width="900" alt="Screenshot 2024-05-08 at 11 47 07 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3ef8ea2c-2198-4ecb-864e-be54e0071739">
<img width="897" alt="Screenshot 2024-05-08 at 11 52 02 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/76436884-3ced-457d-92f2-7af39a41f41a">

# **Pagination**
6 entries exist for Citizen table
<img width="930" alt="Screenshot 2024-05-08 at 1 37 12 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d807ac18-e0dc-4ccf-8967-afd4ab6163b7">

Set starting index and maximum no of results that can be fetched
<img width="1014" alt="Screenshot 2024-05-08 at 1 36 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cf3486c8-2cb5-4ecc-92d1-5cd52bf6b5da">

Retrieved batchwise as per the configuration done using setMaxResult and setFirstResult
<img width="1314" alt="Screenshot 2024-05-08 at 1 39 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9fbd36b5-d63a-44fe-b160-b3dddfc64026">

