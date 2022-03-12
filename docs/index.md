## Module 08

Abir Zaher Mar/11

### Classes and Objects

Classes are object-oriented and are used to create and manage new objects and support inheritance

Here's my code for module 08
```markdown


# ------------------------------------------------------------------------ #
# Title: Assignment 08
# Description: Working with classes

# ChangeLog (Who,When,What):
# RRoot,1.1.2030,Created started script
# RRoot,1.1.2030,Added pseudo-code to start assignment 8
# <Abir Zaher>,<Mar-8>,Modified code to complete assignment 8
# ------------------------------------------------------------------------ #

# Data -------------------------------------------------------------------- #
strFileName = 'products.txt'
lstOfProductObjects = []
choice_str = ""


class Product:
    """Stores data about a product:

    properties:
        product_name: (string) with the products's  name
        product_price: (float) with the products's standard price
    methods:
    changelog: (When,Who,What)
        RRoot,1.1.2030,Created Class
        <Your Name>,<Today's Date>,Modified code to complete assignment 8
    """

    # create constructor
    def __init__(self, prod_name, prod_price):
        # Attributes
        self.__prod_name = str(prod_name)
        self.__prod_price = str(prod_price)

    # create properties
    # Product Name

    @property
    # getters
    def prod_name(self):
        # title case
        return str(self.__prod_name).title()

    # setters
    @prod_name.setter
    def prod_name(self, value):
        # find match for property's name
        if str(value).isnumeric() == False:
            self.__prod_name = value
        else:
            raise Exception("Names Cannot Be Numbers")

    # Product Price

    @property
    # getters
    def prod_price(self):
        # title case
        return str(self.__prod_price).title()

    # setter
    @prod_price.setter
    def prod_price(self, value):
        if str(value).isnumeric():
            self.__prod_price = str(value)
        else:
            raise Exception("Prices must be numbers")

    # Methods

    def to_string(self):
        """ alias of __str__(), converts product data to string """
        return self.__str__()

    def __str__(self):
        """ Converts product data to string """
        return self.prod_name + "," + str(self.prod_price)


class FileProcessor:
    """Processes data to and from a file and a list of product objects:

    methods:
        save_data_to_file(file_name, list_of_product_objects):

        read_data_from_file(file_name): -> (a list of product objects)

    changelog: (When,Who,What)
        RRoot,1.1.2030,Created Class
        <Your Name>,<Today's Date>,Modified code to complete assignment 8
    """

    @staticmethod
    def save_data_to_file(file_name, list_of_product_objects):
        # open file
        obj_file = open(file_name, "w")
        # create list of tasks and priorities
        for objRow in list_of_product_objects:
            obj_file.write(objRow.prod_name + "," + objRow.prod_price + "\n")
        # close file
        obj_file.close()

        return list_of_product_objects

    @staticmethod
    def read_data_from_file(file_name):

        try:
            objFile = open(file_name, "r")
            for line in objFile:
                product, price = line.split(",")
                lstOfProductObjects.append(Product(product.strip(), float(price.strip())))

            return lstOfProductObjects
        except:

            return lstOfProductObjects


# Processing  ------------------------------------------------------------- #

# Presentation (Input/Output)  -------------------------------------------- #
class IO:
    """Display a menu of choices to the user"""

    @staticmethod
    # create a menu for user to choose from
    def output_menu():
        print('''
            Menu of Options
            1) Show current data
            2) Add a new item
            3) Save data to file
            4) Exit program
            ''')
        print()  # an extra line for looks

    @staticmethod
    # ask the user to enter choice
    def input_menu_choice():
        choice = str(input("Which option would you like to perform? [1 to 4] - ")).strip()
        print()  # extra line for looks
        return choice

    @staticmethod
    def output_current_list(list_of_objects):
        # display current list of products and prices
        print("********The Current Products and Prices in the list are:*******")
        for object in list_of_objects:
            print(object)
        print("***************************************************************")
        print()  # an extra line for looks

    @staticmethod
    def input_new_product():
        new_product = input("\nEnter the name of a product: ")
        new_price = float(input("\nEnter the price of the product: "))

        return Product(new_product, new_price)


# Main Body of Script  ---------------------------------------------------- #
# Load data from file
lstOfProductObjects = FileProcessor.read_data_from_file(strFileName)

while True:
    # display menu for user
    IO.output_menu()
    # Get user's menu
    choice_str = IO.input_menu_choice()

    if choice_str == '1':
        # Show user current data in the list of product objects
        IO.output_current_list(lstOfProductObjects)

    elif choice_str == '2':
        # the user adds data to the list of product objects
        addProduct = IO.input_new_product()
        lstOfProductObjects.append(addProduct)

    elif choice_str == '3':
        # saving data to a file
        FileProcessor.save_data_to_file(strFileName, lstOfProductObjects)
        print("Data saved to file!")

    elif choice_str == '4':
        # exit program
        print("Thank you!")
        break

    else:
        print("Error!  Please enter one of the menu options.")
