Consider the following, 
![image](https://github.com/Malobika8/GitDemo/assets/111234135/f4642947-378b-4082-8da6-7fe999baac0c)

* *@Controller annotation:* We can annotate classic controllers with the @Controller annotation. This is simply a specialization of the
  @Component class, which allows us to auto-detect implementation classes through the classpath scanning. We typically use @Controller in
  combination with a @RequestMapping annotation for request handling methods.

  <img width="1148" alt="Screenshot 2024-05-27 at 3 55 51 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/356d7db9-8b40-4a76-a109-57fa06fbb333">

* *@RequestMapping annotation:* One of the most important annotations in spring is the @RequestMapping Annotation which is used to map HTTP
  requests to handler methods of MVC and REST controllers. In Spring MVC applications, the DispatcherServlet (Front Controller) is
  responsible for routing incoming HTTP requests to handler methods of controllers. When configuring Spring MVC, you need to specify the
  mappings between the requests and handler methods. To configure the mapping of web requests, we use the @RequestMapping annotation. The
  @RequestMapping annotation can be applied to class-level and/or method-level in a controller. The class-level annotation maps a specific
  request path or pattern onto a controller. You can then apply additional method-level annotations to make mappings more specific to
  handler methods.

* *@ResponseBody annotation:* The @ResponseBody annotation tells a controller that the object returned is automatically serialized into
  JSON and passed back into the HttpResponse object. When you use the @ResponseBody annotation on a method, Spring converts the return value
  and writes it to the HTTP response automatically. Each method in the Controller class must be annotated with @ResponseBody.

  <img width="855" alt="Screenshot 2024-05-27 at 4 02 01 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/210a6372-05cf-484b-ba97-89ede034174a">

  We need to enable Component Scan

  <img width="1012" alt="Screenshot 2024-05-27 at 4 16 02 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/de2ccb16-d5c1-4afb-8e5c-c8ea1f36a391">

  <img width="1183" alt="Screenshot 2024-05-27 at 4 06 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/cdb74cbe-9bd8-4124-ab06-48955b429cb1">

  **Note:** One controller can have multiple request handlers.
  <img width="1143" alt="Screenshot 2024-05-27 at 7 19 55 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/71acef70-5be6-4dba-bc65-22db1c8a9c07">
  <img width="955" alt="Screenshot 2024-05-27 at 7 20 30 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/71aa2597-44fc-4939-94bb-ddd6de0d08b3">

  RequestMapping can be added at class level as well.

  <img width="992" alt="Screenshot 2024-05-27 at 7 23 36 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/42306918-26e6-49a6-ba64-058fe10ac749">

  

