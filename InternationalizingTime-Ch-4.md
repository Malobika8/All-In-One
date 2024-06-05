# Internationalizing Time (I18N with Time)

The display format of the time differs from one region to another, so we need to internationalize the time. For internationalizing the time, the DateFormat class provides some useful 
methods.

The getTimeInstance() method of the DateFormat class returns the instance of the DateFormat class for the specified style and locale.

Syntax of the getTimeInstance() method is given below:

    public static DateFormat getTimeInstance(int style, Locale locale)

### Example of Internationalizing Time

In this example, we are displaying the current time for the specified locale. The format() method of the DateFormat class receives date object and returns the formatted and localized 
time as a string. Notice that the object of Date class prints date and time both.

<img width="952" alt="Screenshot 2024-06-05 at 1 33 04 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/e782bd58-39a2-4070-b1d1-2517e2500feb">
<img width="1248" alt="Screenshot 2024-06-05 at 2 00 33 PM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3177af35-b31b-4488-8ffc-ff5e3584f327">

