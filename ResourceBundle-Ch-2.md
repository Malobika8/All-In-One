# ResourceBundle Class

The ResourceBundle class is used to internationalize the messages. In other words, we can say that it provides a mechanism to globalize the messages. The hardcoded message is not 
considered good in terms of programming, because it differs from one country to another. So we use the ResourceBundle class to globalize the massages. The ResourceBundle class loads 
these informations from the properties file that contains the messages.

Conventionally, the name of the properties file should be filename_languagecode_country code for example MyMessage_en_US.properties.

### Commonly used methods of ResourceBundle class
There are many methods in the ResourceBundle class. Let's see the commonly used methods of the ResourceBundle class.

- public static ResourceBundle getBundle(String basename) : returns the instance of the ResourceBundle class for the default locale.
- public static ResourceBundle getBundle(String basename, Locale locale) : returns the instance of the ResourceBundle class for the specified locale.
- public String getString(String key) : returns the value for the corresponding key from this resource bundle.

**Example:**

To implement, we would require Locale and ResourceBundle. These belongs to **java.util** package. By defult the language followed is English and country Us.
Create properties file. This file should have key-value pair.

<img width="560" alt="Screenshot 2024-06-05 at 12 39 54 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/247a2472-c9b6-471e-a6e3-8bd4d345b458">
<img width="1002" alt="Screenshot 2024-06-05 at 12 40 12 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/df9e394c-db8c-44fc-97f9-e4508776cdee">
<img width="977" alt="Screenshot 2024-06-05 at 12 40 21 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/d95d7c68-d201-4e50-9da6-755edacea483">

*Note:* language and country is automatically appended to the resource bundle properties file name.

Example: Lang = hi (hindi), Country = "IN" (India), Bundle Name = resourceBundle
    
  The name of the properties file will be \<Bundle-Name\>_\<Lang\>_\<Country\> (in our case, name would be "resourceBundle_hi_IN").
