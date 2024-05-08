<img width="1021" alt="Screenshot 2024-05-07 at 11 35 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/56356bd6-11b3-4f7d-b3f9-d70fee343f8e">

**By default, hibernate uses lazy fetching technique. However, it can changed by adding parameter "fetch=FetchType.EAGER" with the OneToMany annotation.**

1) **Lazy:** It fetches only what is required and doesn't fetch other data. 
      Eg. Consider Question and Answer as two entities. One question can have multiple answers. So, there would be OneToMany mapping associated. Now, when question related data is 
      fetched, intially, only the data required will be pulled. For example, question has id, question description and mutilple answers. But if question id and description is required,
      only those two will be fetched and not answers list although that is part of the question object returned.

  <img width="922" alt="Screenshot 2024-05-08 at 9 14 42 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9b1983ca-d804-4eb9-9267-b0a6838f60f5">
  <img width="899" alt="Screenshot 2024-05-08 at 9 12 40 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9cb10c2d-32bb-41b0-be5a-d2cf58334e68">
  <img width="858" alt="Screenshot 2024-05-08 at 9 13 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a1bc4dcd-0863-41da-a84c-0f5c2ee64f20">
  <img width="899" alt="Screenshot 2024-05-08 at 9 27 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9a8c3984-f043-42f8-be56-e90fc62cb7f6">
  <img width="901" alt="Screenshot 2024-05-08 at 9 28 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/fc98adec-64cf-486a-a25f-09b0845b1194">
      


2) **Eager:** It fetches all data well in advance even if all of it is not required.
       Eg. If we consider the above entities, even when only question id and description is required, it fetches answers list as well because its part of the question object and
       might be required later.
       
  <img width="906" alt="Screenshot 2024-05-08 at 9 28 59 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/06e0c33c-9fea-48da-ad5c-f6a17d5b0e4e">
  <img width="881" alt="Screenshot 2024-05-08 at 9 31 03 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e3136087-9902-429c-acd5-81da57c305ef">
  <img width="903" alt="Screenshot 2024-05-08 at 9 31 37 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/16b0fbd6-cec8-4228-8e80-88dd9c447c7f">
  <img width="901" alt="Screenshot 2024-05-08 at 9 31 46 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ef51cab8-ad0d-409f-87cf-42313d8e9864">

# **Pagination**
6 entries exist for Citizen table
<img width="930" alt="Screenshot 2024-05-08 at 1 37 12 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d807ac18-e0dc-4ccf-8967-afd4ab6163b7">

Set starting index and maximum no of results that can be fetched
<img width="1014" alt="Screenshot 2024-05-08 at 1 36 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cf3486c8-2cb5-4ecc-92d1-5cd52bf6b5da">

Retrieved batchwise as per the configuration done using setMaxResult and setFirstResult
<img width="1314" alt="Screenshot 2024-05-08 at 1 39 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9fbd36b5-d63a-44fe-b160-b3dddfc64026">

