# Internationalizing Number (I18N with Number)

The representation of the numbers differ from one locale to another. Internationalizing the numbers is good approach for the application that displays the informations according to the
locales.

The NumberFormat class is used to format the number according to the specific locale. To get the instance of the NumberFormat class, we need to call either getInstance() or getNumberInstance() methods.

Syntax of these methods is given below:

    public static NumberFormat getNumberInstance(Locale locale)  
    public static NumberFormat getInstance(Locale locale)//same as above  
    
### Example of Internationalizing Number

In this example, we are internationalizing the number. The format method of the NumberFormat class formats the double value into the locale specific number.

<img width="963" alt="Screenshot 2024-06-05 at 1 45 00 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/340288d8-108c-41a8-8302-9157b4d08e30">
<img width="1304" alt="Screenshot 2024-06-05 at 1 59 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/5b8a0dc7-0ed1-4fe1-b149-e7a2a73eb650">

