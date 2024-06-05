# Internationalizing Currency (I18N with Currency)

As we have internationalize the date, time and numbers, we can internationalize the currency also. The currency differs from one country to another so we need to internationalize the 
currency.

The NumberFormat class provides methods to format the currency according to the locale. The getCurrencyInstance() method of the NumberFormat class returns the instance of the 
NumberFormat class.

The syntax of the getCurrencyInstance() method is given below:

    public static NumberFormat getCurrencyInstance(Locale locale)  
    
### Example of Internationalizing Currency
In this example, we are internationalizing the currency. The format method of the NumberFormat class formats the double value into the locale specific currency.

<img width="977" alt="Screenshot 2024-06-05 at 1 54 26 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/71f5fecd-b219-4183-a54e-3cb1abe67f02">
<img width="1193" alt="Screenshot 2024-06-05 at 1 58 38 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/a40991f4-1bcd-41f6-ace9-68af2ece3c1b">

