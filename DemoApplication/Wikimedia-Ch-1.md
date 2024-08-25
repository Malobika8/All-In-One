## What is Wikimedia?

It's a group of services.

<img width="1031" alt="Screenshot 2024-08-25 at 12 13 55 PM" src="https://github.com/user-attachments/assets/e676e934-f829-4255-aca3-ac568ff246c7">

Wikimedia is a nonprofit organization that hosts free knowledge projects, including Wikipedia and Wikimedia Commons. The Wikimedia Foundation's 
goal is to make it easier for people to share what they know by providing reliable, fast, and accessible sites. The foundation also supports 
the communities of volunteers who contribute to the projects. 

Here are some of the projects that Wikimedia hosts: 
- Wikipedia: A free online encyclopedia written in more than 300 languages by volunteers around the world. 
- Wikimedia Commons: A free library of illustrations, photos, drawings, videos, and music. Wikimedia Commons also hosts the Picture of the
  Year (POTY) competition, which identifies the best freely licensed images from the site. 
- Wikidata: A set of structured data.
  
The Wikimedia Foundation was established in 2003 and is powered by donations from individuals. 

"*stream.wikimedia*" is a stream that represents all the changes that are made by the community on the wikimedia projects. We can see all the
recent changes by hitting the below endpoint,

```
https://stream.wikimedia.org/v2/stream/recentchange
```

<img width="1143" alt="Screenshot 2024-08-25 at 12 19 04 PM" src="https://github.com/user-attachments/assets/18f4d77b-210b-4b45-a22e-6a2934596d53">

We can see overview of streams as well.

<img width="1075" alt="Screenshot 2024-08-25 at 12 20 05 PM" src="https://github.com/user-attachments/assets/0776fa50-9414-44df-ba42-89e10c1e2c06">

This is a huge stream & in order to be able to process that we need a strong, scalable & powerful message broker like Apache Kafka.
