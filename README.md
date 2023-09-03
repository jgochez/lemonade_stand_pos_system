# Lemonade Stand Point of Service (POS) System

You will be writing code for a simulator that records the menu items and daily sales of a lemonade stand. It will have these classes: MenuItem, SalesForDay, and LemonadeStand. All data members of each class should be marked as **private** (a leading underscore in the name). Since they're private, if you need to access them from outside the class, you should do so via get or set methods.

Here are descriptions of the three classes:


**MenuItem:**

A MenuItem object represents a menu item to be offered for sale at the lemonade stand. It has three data members:
* a string for the item's name
* a float for the item's wholesale cost (how much the stand pays for the item)
* a float for the item's selling price (how much the stand sells the item for)

The Menu Item methods are:
* init method - takes three parameters (name, wholesale cost, selling price) and uses them to initialize the data members
* get methods for each of the data members: get_name(), get_wholesale_cost(), and get_selling_price()


**SalesForDay:**

A SalesForDay object represents the sales for a particular day. It has two data members:
* an integer for the number of days the stand has been open so far
* a dictionary whose keys are the names of the items sold and whose values are the numbers of those items sold that day

The SalesForDay methods are:
* init method - takes two parameters (number of days, sales dictionary) and uses them to initialize the data members
* get methods for each of the data members: get_day() and get_sales_dict()


**LemonadeStand:**
**Remember that the LemonadeStand class must not directly access the private data members of MenuItem and SalesForDay objects, but instead must call the appropriate get methods**

A LemonadeStand object represents a lemonade stand. It has four data members: 
* a string for the name of the stand
* an integer representing the current day
* a dictionary of MenuItem objects, where the keys are the names of the items and the values are the corresponding MenuItem objects
* a list of SalesForDay objects

The LemonadeStand methods are:
* init method - takes one parameter, a string for the name of the stand; initializes the name to that value, initializes current day to zero, initializes the menu to an empty dictionary, and initializes the sales record to an empty list
* a get method for the name: get_name()
* add_menu_item:
  * Takes as a parameter a MenuItem object and adds it to the menu dictionary
  * New items can be added to the menu on any day
* enter_sales_for_today:
  * Takes as a parameter a dictionary where the keys are names of items sold and the corresponding values are how many of the item were sold (see the example at the end of the readme)
  * If an item in the menu doesn't appear in the dictionary, then there were no sales of that item on that day. You don't need to worry about this in this method, but it's important in the next method.
  * If the name of **any** item sold doesn't match the name of any MenuItem in the dictionary of MenuItem objects, this method should do nothing except raise an **InvalidSalesItemError** (you'll need to define this exception class)
  * Otherwise, it should create a new SalesForDay object using the current day and the dictionary that was passed in, add that object to the list of SalesForDay objects, and then increment the current day by 1
  * Any time this method is called (and the exception isn't raised), **exactly one** SalesForDay object should be created and added to the list
* sales_of_menu_item_for_day:
  * Takes as parameters an integer representing a particular day and a string for the name of a menu item
  * Returns the number of that item sold on that day
  * This method uses the given day to find the corresponding SalesForDay object in the list and then calls its get_sales_dict() method to get the dictionary of sales for that day
  * Then looks for the item name in the dictionary, taking into account that if an item in the menu doesn't appear in the dictionary, then there were no sales of that item on that day
* total_sales_for_menu_item:
  * Takes as a parameter a string for the name of a menu item and returns the total number of that item sold over the history of the stand
  * This method can make use of sales_of_menu_item_for_day
* total_profit_for_menu_item:
  * Takes as a parameter a string for the name of a menu item and returns the total profit on that item over the history of the stand
  * The profit for any item sold is the selling price of the item minus the wholesale cost of the item
  * This method can make use of total_sales_for_menu_item
* total_profit_for_stand:
  * Takes no parameters and returns the total profit on all items sold over the history of the stand
  * This method can make use of total_profit_for_menu_item
  
So a LemonadeStand contains a **dictionary** of MenuItems. It also contains a **list** of SalesForDay objects, and each of those SalesForDay objects contains a **dictionary** of items sold on a particular day. At each point it's important to keep straight whether you are currently working with a list or a dictionary, which you may find trickier when one is nested inside the other. 


**Your main file must include a main function** that runs if the file is run as a script, but not if it's imported to another file.  Your main function should:
1. create a LemonadeStand object
2. create one or more MenuItem objects and add them to the LemonadeStand's menu
3. create a dictionary of sales for the day that includes sales of at least one item that isn't in the menu
4. try calling enter_sales_for_today(), passing that sales dictionary as the argument
5. If an InvalidSalesItemError is raised, it should be caught with a try/except that prints an explanatory message for the user (otherwise the function should proceed normally)

In addition to your file containing the code for the above classes, **you must also submit a file that contains unit tests for your classes.  It must have at least five unit tests and use at least two different assert functions.  This part (like the rest) must be your own work. 


