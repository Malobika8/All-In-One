# Internationalization and Localization in Java

Internationalization is also abbreviated as I18N because there are total 18 characters between the first letter 'I' and the last letter 'N'. Internationalization is a mechanism to 
create such an application that can be adapted to different languages and regions.
Internationalization is one of the powerful concept of java if you are developing an application and want to display messages, currencies, date, time etc. according to the specific 
region or language.

Localization is also abbreviated as I10N because there are total 10 characters between the first letter 'L' and last letter 'N'. Localization is the mechanism to create such an 
application that can be adapted to a specific language and region by adding locale-specific text and component.

**Before starting the internationalization, Let's first understand what are the informations that differ from one region to another. There is the list of culturally dependent data:**

- Messages
- Dates
- Times
- Numbers
- Currencies
- Measurements
- Phone Numbers
- Postal Addresses
- Labels on GUI components etc.

**Importance of Locale class in Internationalization:**

An object of Locale class represents a geographical or cultural region. This object can be used to get the locale specific information such as country name, language, variant etc.

### Fields of Locale class
There are fields of Locale class:

- public static final Locale ENGLISH
- public static final Locale FRENCH
- public static final Locale GERMAN
- public static final Locale ITALIAN
- public static final Locale JAPANESE
- public static final Locale KOREAN
- public static final Locale CHINESE
- public static final Locale SIMPLIFIED_CHINESE
- public static final Locale TRADITIONAL_CHINESE
- public static final Locale FRANCE
- public static final Locale GERMANY
- public static final Locale ITALY
- public static final Locale JAPAN
- public static final Locale KOREA
- public static final Locale CHINA
- public static final Locale PRC
- public static final Locale TAIWAN
- public static final Locale UK
- public static final Locale US
- public static final Locale CANADA
- public static final Locale CANADA_FRENCH
- public static final Locale ROOT

### Constructors of Locale class
There are three constructors of Locale class.They are as follows:

- Locale(String language)
- Locale(String language, String country)
- Locale(String language, String country, String variant)

### Commonly used methods of Locale class
There are given commonly used methods of Locale class:

- public static Locale getDefault() it returns the instance of current Locale
- public static Locale[] getAvailableLocales() it returns an array of available locales.
- public String getDisplayCountry() it returns the country name of this locale object.
- public String getDisplayLanguage() it returns the language name of this locale object.
- public String getDisplayVariant() it returns the variant code for this locale object.
- public String getISO3Country() it returns the three letter abbreviation for the current locale's country.
- public String getISO3Language() it returns the three letter abbreviation for the current locale's language.

Example of Local class that prints the informations of the default locale. In this example, we are displaying the informations of the default locale. If you want to get the 
informations about any specific locale, comment the first line statement and uncomment the second line statement in the main method.

    import java.util.*;  
    
    public class LocaleExample {  
      public static void main(String[] args) {  
    
        Locale locale=Locale.getDefault();  
        //Locale locale=new Locale("fr","fr");//for the specific locale  
  
        System.out.println(locale.getDisplayCountry());  
        System.out.println(locale.getDisplayLanguage());  
        System.out.println(locale.getDisplayName());  
        System.out.println(locale.getISO3Country());  
        System.out.println(locale.getISO3Language());  
        System.out.println(locale.getLanguage());  
        System.out.println(locale.getCountry());  
      
      }  
    }  

Output:

       United States
       English
       English (United States)
       USA
       eng
       en
       US
