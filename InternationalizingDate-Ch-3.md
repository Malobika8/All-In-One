# Internationalizing Date (I18N with Date)

The format of the dates differ from one region to another that is why we internationalize the dates. We can internationalize the date by using the getDateInstance() method of the
DateFormat class. It receives the locale object as a parameter and returns the instance of the DateFormat class.

### Commonly used methods of DateFormat class for internationalizing date
There are many methods of the DateFormat class. Let's see the two methods of the DateFormat class for internationalizing the dates.

- public static DateFormat getDateInstance(int style, Locale locale) : returns the instance of the DateFormat class for the specified style and locale. The style can be DEFAULT,
  SHORT, LONG etc.
- public String format(Date date) : returns the formatted and localized date as a string.


### Example of Internationalizing Date
In this example, we are displaying the date according to the different locale such as CANADA, TAIWAN, ENGLISH etc. For this purpose we have created the print() method that receives 
Locale object as an instance. The format() method of the DateFormat class receives the Date object and returns the formatted and localized date as a string.

<img width="995" alt="Screenshot 2024-06-05 at 1 19 12 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/ecaca097-9c1d-4d1c-a7d7-169424b025ea">
<img width="1261" alt="Screenshot 2024-06-05 at 2 00 22 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/aecf48ad-67bf-40bf-8399-70b3570fe822">



