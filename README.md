# Book-Library
import datetime                                                                                     # importing the datetime module to get the borrow and the return date

class Book_Library:
    def __init__(self, lend_book_list, lend_book_price, add_book_list, add_book_price, return_book_list, return_user_code, user_work, name, code, contact_no, address, vip_code, membership_options):
        self.lendBookList = lend_book_list
        self.lendBookPrice = lend_book_price
        self.addBookList = add_book_list
        self.addBookPrice = add_book_price
        self.returnBookList = return_book_list
        self.returnUserCode = return_user_code
        self.userWork = user_work
        self.name = name
        self.code = code
        self.contact_no = contact_no
        self.address = address
        self.vip_code = vip_code
        self.membership_options = membership_options


    def display_book(self):
        """to print name of all the books and number of books present  """
        if self.userWork == 1 or self.userWork == 2:
            print("\n\t\t\t\t\t\t\tLIST OF RENTING BOOKS ")
            print("BOOK CODE\t\t\t\t\tBOOK NAME \t\t\t\t\tPRICE")
            for key in self.lendBookList:
                print(f"\t {key}  \t\t\t\t\t\t   {self.lendBookList[key]} \t\t\t\t Rs. {self.lendBookPrice[key]}")  ######## Have to hide the "none" coming in the book list4

        if self.userWork == 1 or self.userWork == 3:
            print("\n\t\t\t\t\t\tLIST OF PURCHASEABLE BOOKS ")
            print("BOOK CODE \t\t\t\t\t  BOOK NAME  \t\t\t\t\t  PRICE")
            for key in self.addBookList:
                print(f"\t {key}  \t\t\t\t\t\t\t\t {self.addBookList[key]} \t\t\t\t\t\t Rs. {self.addBookPrice[key]}")


    def lend_book(self):
        book_available = input("\nIs the customer desired book available : ")
        if book_available == "YES":
            book_no = int(input("Enter the book serial number : "))

            #using the datetime modules to get the date and time of the borrow and the return of the book
            current_date = datetime.datetime.now().replace(microsecond=0)
            if vip_access == "YES":
                return_date = datetime.datetime.now().replace(microsecond=0) + datetime.timedelta(days=30)
            else:
                return_date = datetime.datetime.now().replace(microsecond=0) + datetime.timedelta(days=15)

            print(f"\n\t\t\t\t\t\t\t BILL\n\n "
                   f"Customer Details : \n"
                   f"\tCustomer Name                            =     {self.name}\n "
                   f"\tContact Number                            =     {self.contact_no}\n "
                   f"\tAddress                                         =     {self.address}\n\n"
                   f" Purchase Details : \n"
                   f" \tBook Name                                    =     {self.lendBookList[book_no]}\n "
                   f"\tTotal Amount                                 =    Rs. {self.lendBookPrice[book_no]}\n "
                   f"\tBorrowing Date and Time              =    {current_date}\n"
                   f"\tReturning Date and Time               =    {return_date} \n"
                   f"\nThanks For Visiting.")
            
            # book rented and the name of the person is stored in the r_book_list
            self.returnBookList.update({self.lendBookList.get(book_no): self.name}) 
            self.returnUserCode.update({self.code: self.name})
            self.lendBookList.pop(book_no)                                                                                                                       # the book is popped out of the l_book_list and L_book_price so that the option of renting these book
            self.lendBookPrice.pop(book_no)                                                                                                                              # would not be shown to any other person

        elif book_available == "NO":
            book_name = input("Enter the name of the wanted book: ")
            if book_name in r_book_list:
                print("The wanted book is borrowed by someone else.")
            else:
                ask_order = input("Do the customer want to request for the special order of the book with extra charges : ")
                if ask_order == "YES":
                    book_desired = input("Enter name of the wanted book : ")
                    print(f"{book_desired} added to the Requested Book Database. ")
                else:
                    print("OK")
        else:
            print("Please type a valid input.")


    def add_book(self):
        book_available = input("\nIs the book customer wanted to sell available :  ")
        if book_available == "YES":
            book_code = int(input("Enter the book code : "))
            if book_code in self.addBookList:
                price_acceptable = input("Is the price offered acceptable to the customer : ")
                if price_acceptable == "YES":
                    lending_price = int(input("Enter the lending price of the bought book (provided by librarian only ) : "))                                       # a lending price is asked so that the rent price of the book can be added to the l_book_price
                    self.lendBookList.update({len(self.lendBookList)+1: self.addBookList[book_code]})
                    self.lendBookPrice.update({len(self.lendBookPrice)+1: lending_price})
                    print(f" \nThanks for selling the book to us. Here is your bill.\n"
                           f"\n\t\t\t\t\t\t\t\t\t BILL\n "
                           f"Customer Details : \n"
                           f"\tCustomer Name                            =     {self.name}\n "
                           f"\tContact Number                            =     {self.contact_no}\n "
                           f"\tAddress                                         =     {self.address}\n\n"
                           f" Selling Details : \n"
                           f" \tBook Name                                    =     {self.addBookList[book_code]}\n "
                           f"\tAmount Given                                =    Rs. {self.addBookPrice[book_code]}\n ")
                    self.addBookList.pop(book_code)
                    self.addBookPrice.pop(book_code)
                elif price_acceptable == "NO":
                    print("Sorry but we cannot offer you more than the price offered.")
                else:
                    print("Please enter a valid input")
            else:
                print("Please enter a valid input.")
        elif book_available == "NO":
            book_name = input("Enter the name of book : ")
            print(f"Sorry, we cannot buy {book_name} now but we'll contact the customer if we are in the need of the book. ")
        else:
            print("Please enter a valid input.")

    def return_book(self):
        if self.code not in self.returnUserCode:
            print("\nThis user code does not belong to any customer in Return Book Database.")
        else:
            book_name = input("Enter the book name : ")
            if book_name in self.returnBookList:
                self.returnBookList.pop(book_name)
                self.returnUserCode.pop(self.code)
                print("\nThanks for returning the book.\nCustomer Details and Book Name removed from the ReturnBook Database.")
            else:
                print(self.returnBookList)
                print("The book name is wrong. Please check")

    def purchase_membership(self):
        print("\n\t\t\t\t\tVIP Membership Options :-\n  ")                                                                  # for printing the list of VIP Membership packages
        print("DURATION\t\t\t\t\t\tPRICE")
        for key in self.membership_options:
            print(f"{key}\t\t\t\t\t\t\tRs. {self.membership_options[key]}")

        list_days = []                                                                                                                            # for appending the keys and values of membership_options dictionary into separate list for ease in use
        list_price = []                                                                                                                           # list_days contains the durations of the membership
        for i in self.membership_options:                                                                                           # list_price contains the price of each membership
            list_days.append(i)
            list_price.append(self.membership_options[i])

        chosen_package = int(input("\nPlease enter the desired package serial number : "))                          # asking the user's choice as input
        if chosen_package in [1, 2, 3, 4, 5]:
            l = len(vip_user_code)
            vip_code_list = []
            for key in vip_user_code:
                vip_code_list.append(key)
            self.vip_code.update({vip_code_list[l - 1] + 1: self.name})
            print(f" \nThanks for becoming a member of the National Library.\n"
                  f"\n\t\t\t\t\t\t\t\t\t BILL\n "
                  f"Customer Details : \n"
                  f"\tVIP Code                                        =    {vip_code_list[l - 1] + 1}\n"
                  f"\tCustomer Name                            =     {self.name}\n "
                  f"\tContact Number                            =     {self.contact_no}\n "
                  f"\tAddress                                         =     {self.address}\n\n"
                  f" Selling Details : \n"
                  f" \tMembership Duration                  =     {list_days[chosen_package - 1]}\n "
                  f"\tMembership Price                         =    Rs.{list_price[chosen_package - 1]}\n ")
            print("* From now please use the entered user name and the provided VIP Code to use the VIP Access.")
        else:
            print("Please enter a valid input.")




if __name__ == '__main__':

    l_book_list = {1: "HARRY POTTER 1", 2: "HARRY POTTER 2", 3: "HARRY POTTER 3", 4: "HARRY POTTER 4",
                   5: "HARRY POTTER 5", 6: "HARRY POTTER 6", 7: "HARRY POTTER 7"}
    l_book_price = {1: 110, 2: 140, 3: 120, 4: 160, 5: 180, 6: 200, 7: 250}
    a_book_list = {1: "BOOK 1", 2: "BOOK 2", 3: "BOOK 3", 4: "BOOK 4", 5: "BOOK 5", 6: "BOOK 6", 7: "BOOK 7"}
    a_book_price = {1: 300, 2: 500, 3: 570, 4: 350, 5: 250, 6: 400, 7: 600}
    r_book_list = {}                                                                                                 # format --> book name : customer name
    r_user_code = {}                                                                                                 # format --> user code : customer name
    vip_membership = {"28 DAYS": 199, "84 DAYS": 499, "168 DAYS": 899, "336 DAYS": 1799, "672 DAYS": 3999}
    vip_user_code = {1001: "PERSON A", 1002: "PERSON B", 1003: "PERSON C", 1004: "PERSON D", 1005: "PERSON E", 1006: "PERSON F"}


    while True:
        print("____________________________________________________________________________________________________________________________________________")
        print("\nWelcome to the National Library. Please type the input in capital letters.\n")
        print("Customer's purpose of visit : \n1. See the book list \n2. Lend a book \n3. Sell a book \n4. Return a book\n5. Buy VIP Membership\n")

        user_purpose = input("Enter the option : ")
        if user_purpose not in ['1', '2', '3', '4', '5']:
            print("Please type a valid option\n")
            continue
        else:
            user_purpose = int(user_purpose)

        print("\nPlease enter the customer details : ")

        if user_purpose == 2 or user_purpose == 3:
            vip_access = input("Are you a VIP Member : ")
            if vip_access == "YES" or vip_access == "NO":
                pass
            else:
                print("Please type a valid input.")
                continue
        else:
            vip_access_list = ["YES", "NO"]
            vip_access = vip_access_list[1]

        user_name = input(" Name : ")
        user_code = int(input(" Code : "))

        if vip_access == "YES":
            if user_code in vip_user_code and user_name == vip_user_code[user_code]:
                pass
            elif user_code in vip_user_code and user_name != vip_user_code[user_code]:
               print("User Name does not match with VIP Access Code provided.")
               continue
            elif user_code not in vip_user_code:
                print("VIP Access Code does not match.")
                continue
        elif vip_access == "NO":
            if user_code in vip_user_code:
                print("User Name does not match with VIP Access Code provided.")
                continue
            else:
                pass

        if user_code in r_user_code and user_name != r_user_code[user_code]:
                 print("The Customer Code and Customer Name does not match. Please check ")
                 continue
        if user_code in r_user_code and user_purpose == 2:
            if vip_access == "YES":
                list1 = []
                for values in r_book_list.values():
                    list1.append(values)
                if list1.count(user_name) >= 2:
                    print("The customer cannot borrow more than two books.")
                    continue
                else:
                    pass

            elif vip_access == "NO":
                print("The Customer Code cannot borrow another book before returning another book.")
                print("*********We suggest to buy the VIP membership to borrow more books.**********")
                continue
            else:
                print("Please type a valid input.")
                continue

        user_contact_number = int(input(" Contact Number : "))
        user_address = input(" Address : ")

        user = Book_Library(l_book_list, l_book_price, a_book_list, a_book_price, r_book_list, r_user_code, user_purpose, user_name, user_code, user_contact_number, user_address, vip_user_code, vip_membership)

        if user_purpose == 1:
            user.display_book()

        elif user_purpose == 2:
            user.display_book()
            user.lend_book()

        elif user_purpose == 3:
            user.display_book()
            print(user.add_book())

        elif user_purpose == 4:
            user.return_book()

        elif user_purpose == 5:
            user.purchase_membership()

        else:
            print("Please enter a valid option")

        print("\nPress E to exit and C to continue :- ")
        choice = ' '
        while choice != "E" and choice != "C":
            choice = input("Enter the choice : ")
            if choice == "E":
                exit()
            elif choice == "C":
                continue
            else:
                print("Please type a valid input.")
