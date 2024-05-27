- Consider the following, 
  <img width="972" alt="Screenshot 2024-05-27 at 7 51 53 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/46518c82-95a6-495c-9f41-17969f2f834f">

  If we remove @ResponseBody, whatever is returned is considered as a page name.
  Create a view folder in WEB_INF where we can store our view/web pages. Create a simple web page.

  <img width="1298" alt="Screenshot 2024-05-27 at 8 01 43 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e514e626-94cf-42b2-a04f-017dc3846000">

  We can return the web page from request handler.

  <img width="924" alt="Screenshot 2024-05-27 at 8 04 20 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/2f6e0f24-3796-412e-92e3-2b561751a815">

  Re-run the application and we get a proper web page this time.

  <img width="1257" alt="Screenshot 2024-05-27 at 8 03 03 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b30e43f0-a75c-4228-b07d-cfb603c9a152">

- ViewResolver: Ideally, we should'nt be hardcoding the path of the web page as in Spring MVC, it's not required to return fully qualified path. Instead,
  ViewResolver can be utilized.

  <img width="1119" alt="Screenshot 2024-05-27 at 8 15 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/bca3b679-fd25-4c71-a3f8-1c77e4aec6ba">
  <img width="1155" alt="Screenshot 2024-05-27 at 8 19 09 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/759b2627-b8e7-4c0e-b772-77825c5b8635">

  There is an existing classes called "InternalResourceViewResolver" which extends UrlBasedViewResolver class that has getters and setters
  for "prefix" & "suffix".

  <img width="1142" alt="Screenshot 2024-05-27 at 8 28 17 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3f0e4d91-4321-44fc-95a3-29f0ef29d542">

  Configuration is done in SpringConfiguration(WebApplicationContext) xml file similar to how it is done for other beans.

  <img width="1141" alt="Screenshot 2024-05-27 at 8 29 02 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/eaf300e3-9cd7-43c2-8666-7acb8df9fb48">
  <img width="919" alt="Screenshot 2024-05-27 at 8 40 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/39d3e120-fb85-4348-b9d8-386d026d0b92">
  <img width="919" alt="Screenshot 2024-05-27 at 8 47 09 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e22c04d2-bd58-4ffb-a69d-a9ce176a25ca">
  <img width="1019" alt="Screenshot 2024-05-27 at 8 42 40 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ea984c43-6f01-40e0-b1d2-99251a995b2a">
