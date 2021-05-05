# IntlDate
*JavaScript International Date Object*

> ‼ **NOTE:** This project was migrated from [CodePlex](https://archive.codeplex.com/?p=intldate) and is not maintained. ‼

This is an internationalized implementation of the JavaScript Date object. It enables converting dates between different types of calendars at the client-side. You can also utilize it into your existing and most complex JavaScript date and calendar components with the least effort to support other calendars.

Project Description
-------------------

The primary goal of this project is to develop a JavaScript code base to
support all the localized
[calendars](http://msdn2.microsoft.com/en-us/library/aa903917.aspx) that
are available in .NET Framework 2.0 System.Globalization namespace in
the browser.\
\
This project consists of a base IntlDate object which implements every
setter and getter method that is exposed by a standard [JavaScript Date
object](http://msdn2.microsoft.com/en-us/library/cd9w2te4.aspx). Taking
advantage of JavaScript’s state of being loosely-typed, we can easily
convert a Date object to an IntlDate as soon as it is constructed, and
thereafter all the way into the code flow it is used like a regular Date
object except internally it does the calculatons according to our
calendar type of choice. This allows us to easily convert existing
JavaScript calendar controls to support localized calendars.\
\
**Sample:**\
![datepicker_tbg](https://user-images.githubusercontent.com/767147/117209766-a4c02200-adab-11eb-97c3-9768f4c4937d.gif)
Windows SharePoint Services 2.0 date picker using International Date
object to impersonate dates as Persian calendar dates.\

JavaScript Console
------------------

You can use the browser based JavaScript Console to run your script
snippets and see the outputs right away. I made this application as a
tool to test the International Date object as I was developing it. It is
also great to use to provide a demo of how the International Date Object
works. To begin, open JSConsole.htm.\
\
The following script files are imported to the console by default:\
\
**IntlDateDemo.js:** Contains some functions used specifically for this
demo.\
**IntlDate.js:** Contains the base class for International Date object.\
**Calendars/PersianDate.js:** The PersianDateUTC class which is
inherited from IntlDateBase.\
\
**Note:** At the time of writing this sample, the Persian Date is the
only calendar type that is complete and working. We are going to use the
same techniques to implement other calendar types during this project
and as new date objects are available you can use them in the same way
as the Persian Date is used in this demo.\

Debugger
--------

You can use a script debugger such as Microsoft Visual Studio to step
through the code you’re running inside the JavaScript Console. To enable
script debugging, first you need to enable it in Internet Explorer. Go
to Internet Options, click on Advanced tab and uncheck "Disable Script
Debugging". Then enable the debugger in the JavaScript Console by
checking the "Enable debugger" checkbox. Now the debugger will be
triggered every time you click on the Run button.\

Using IntlDate Object
---------------------

This section will give you a quick overview of using an International
Date object. I have tried to give the samples here as simple as
possible.\
\
1. Type the following lines in the input text box of JavaScript
Console:\
\

    var d;
    d = new Date();

\
\
In the Output box, you will see the toString() return value of object d.
The Output box shows only the string representation of the last line of
code.\
\
2. Now try the following:\
\

    var d;
    d = new PersianDate();

\
\
The above is equivalent to:\
\

    var d;
    d = new PersianDate(new Date());

\
\
and:\
\

    var d;
    var ticks = new Date().getTime();
    d = new PersianDate(ticks);

\
\
3. Back to the native Date object, use the predefined PrintDate() method
to show its properties.\
\

    var d;
    d = new Date();
    PrintDate(d);

\
\
4. Try converting the date object to an IntlDate object (here
PersianDate).\
\

    var d;
    d = new Date();
    d = d.toPersianDate();

\
\
Now d is an IntlDate object but holds the same methods as a regular Date
object. This is also equivalent to what you did in step 2.\
\
There is another way to do this:\
\

    var d;
    d = new Date();
    d = d.localize('Persian');

\
\
You can chain conversions back and forth as many times as you want with
different methods:\
\

    var d;
    d = new Date().toPersianDate().toDate().localize('Persian');

\
\
5. Use PrintDate() method to query the new object.\
\

    var d;
    d = new Date();
    d = d.toPersianDate();
    PrintDate(d);

\
\
You can see the output for each method is calculated by the Persian
calendar.\
\
6. A number is assigned to each calendar type that is derived from
IntlDate. For the Persian date it is 4. You can get the calendar type
number through the object’s caltype field.\
\

    var d;
    d = new Date();
    d = d.toPersianDate();
    Print(d.caltype);

\
\
Here’s the numbering of other calendar types:\
\

  ---- -----------
  1    Gregorian
  4    Persian
  6    Hijri
  7    Buddhist
  8    Hebrew
  16   SakaEra
  22   EastAsian
  24   Japanese
  26   Julian
  28   Korean
  30   Taiwan
  32   UmAlQura
  ---- -----------

\
\
**Note:** Since I initially wanted to make it compatible with Windows
SharePoint Services, for those calendar types that are defined in
Windows SharePoint Services 2.0, I have used the same enumeration
numbers. For the other calendar types, the associated number is selected
randomly and might be changed in the future.\
\
7. Set a default calendar type to be used when localizing a Date object.
You can specify calendar types by their names or by their numbers.\
\

    Calendar.localType = 4; // or 'Persian'
    var d;
    d = new Date();
    d = d.localize();

\
\
8. Use the getName() method to get the name of the calendar type.\
\

    Calendar.localType = 4;
    var d;
    d = new Date().localize();
    d.getName();

\
\
9. You can choose the way numbers are displayed by an International Date
object, by setting the locale digit shape.\
\

    Calendar.localType = 4;
    Calendar.digitShape = 2;
    var d;
    d = new Date().localize();
    d.toLocaleString();

\
\
There are more than 20 digit shaping groups defined in Unicode and you
can try them by specifing their digitShape index. Try other numbers for
digitShape.\
\
The above example is same as this one:\
\

    Calendar.localType = 'Persian';
    Calendar.digitShape = PersianDate.defaultDigitShape;
    var d;
    d = new Date().localize();
    d.toLocaleString();

\
\
**Note:** If you have the Arial Unicode MS universal font installed, you
can view most of the digit characters. To install this font run Office
2003 setup (sorry my info is old here), select Advanced customization
and then select and install:\
Microsoft Office \> Office Shared Features \> International Support \>
Universal Font\
\
10. Another way to create an International Date object is to use its
constructor directly.\
\

    Calendar.localType = 4;
    Calendar.digitShape = 2;
    var d;
    d = new PersianDate(1385, 2, 15, 0, 0, 0);
    d.toLocaleDateString();

\
\
**Note:** When using this constructor, the date and time arguments are
interpreted as local time.\
\
**Note:** Month parameters in IntlDate objects are zero based similar to
the native JavaScript Date object. So in the above code the date is set
to 1385/3/15 Persian. Similar to the following code:\
\

    Calendar.localType = 4;
    Calendar.digitShape = 2;
    var d;
    d = new Date(0).localize();
    d.setFullYear(1385, 2, 15);
    d.toLocaleDateString();

\
\
11. You can also use the base IntlDate class’ constructor and specify
the date parts and the calendar type.\
\

    Calendar.localType = 4;
    Calendar.digitShape = 2;
    var d;
    d = new IntlDate(1385, 2, 15, 0, 0, 0, 'Persian');
    d.toLocaleDateString();

\
\
12. To convert a Gregorian date to a localized date, create a Date
object and use the localize() method.\
\

    Calendar.localType = 'Persian';
    var d;
    d = new Date(2006, 8, 17).localize();
    d.toDateString();

\
\
13. To convert an IntlDate to a Gregorian date, use the toDate()
method.\
\

    var d;
    d = new PersianDate(1385, 2, 15).toDate();
    d.toDateString();

\
\
14. When you are not sure if your date object is a JavaScript Date or an
IntlDate, use the delocalize() method instead. This method is a
prototype of both objects and always returns a standard JavaScript Date
object.\
\

    var d;
    d = new PersianDate(1385, 2, 15).delocalize();
    d.toDateString();

\
\
15. To convert an International Date to another IntlDate object use the
localize() method or any of the other conversion chain methods. For
example to convert a Persian date to a Hindu Saka Era date you can do it
this way:\
\

    var d;
    d = new PersianDate().localize('SakaEra'); // or .localize(16)

\
\
**Note:** Conversions would work only after both calendars are
implemented. The IntlDate base class supports all these conversions,
however, currently only Persian calendar is implemented. Each calendar
only needs to know how to convert to and from a native date object to be
able to convert to any of the other IntlDate calendars. If you care
about any other international calendars to be included please help to
extend this library using the techniques provided.\
\
Other examples:\
\

    d = new Date().localize('Japanese');

\
\

    h = new HijriDate(1434, 1, 1);
    d = new HebrewDate(h);

\
\

    d = new JapaneseDate()
            .toHijriDate()
            .toEastAsianDate()
            .localize('UmAlQura')
            .toDate()
            .localize(28) // Korean
            .localize('Persian')
            .toBuddhistDate() // ...

\
\
Of course in most cases only conversions between two types of calendars
would make sense. The last example above is given only to demonstrate
the possibilities.\

Next Project
------------

Integrate with [Moment.js](http://momentjs.com) ?\

Date and IntlDate Methods Comparison Chart
------------------------------------------

The following table compares the public methods available in Date object
and IntlDate object.\
**x** means available. Methods indicated by **d** are defined by the
IntlDate.js script file.\
\

  Public               Date   IntlDate
  -------------------- ------ ----------
  localize             d      x
  delocalize           d      x
  toDate                      x
  getName                     x
  getDay               x      x
  getFullYear          x      x
  getYear              x      x
  getMonth             x      x
  getDate              x      x
  getHours             x      x
  getMinutes           x      x
  getSeconds           x      x
  getMilliseconds      x      x
  getTime              x      x
  getTimezoneOffset    x      x
  getUTCDay            x      x
  getUTCFullYear       x      x
  getUTCMonth          x      x
  getUTCDate           x      x
  getUTCHours          x      x
  getUTCMinutes        x      x
  getUTCSeconds        x      x
  getUTCMilliseconds   x      x
  getVarDate           x      x
  toDateString         x      x
  toTimeString         x      x
  toString             x      x
  toLocaleDateString   x      x
  toLocaleTimeString   x      x
  toLocaleString       x      x
  toUTCString          x      x
  toGMTString          x      x
  valueOf              x      x
  setDate              x      x
  setFullYear          x      x
  setHours             x      x
  setMilliseconds      x      x
  setMinutes           x      x
  setMonth             x      x
  setSeconds           x      x
  setTime              x      x
  setUTCDate           x      x
  setUTCFullYear       x      x
  setUTCHours          x      x
  setUTCMilliseconds   x      x
  setUTCMinutes        x      x
  setUTCMonth          x      x
  setUTCSeconds        x      x
  setYear              x      x
  UTC                  x      
  parse                x      
