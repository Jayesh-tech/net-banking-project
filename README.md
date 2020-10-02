# net-banking-project
import os


class User_Credentials():
    login_ = False
    current_balance = 0
    root_password = "_"
    name = "JonDoe"
    
    def new_account():
        os.system('cls')
        User_Credentials.name            = input("User Name : ")
        User_Credentials.root_password   = str(input("Password  : "))
        User_Credentials.login_          = True
        user = open("C:\\Users\\Shweta\\Desktop\\UserCredentials\\" + User_Credentials.name, "w+") 
        user.write(User_Credentials.root_password + " " + str(User_Credentials.current_balance))
        main()

    def manage_account():
        print("Hi" + User_Credentials.name)
        print(
        """
Press 1 - change UserName
Press 2 - change Password
        """)

        i = int(input("> "))

        if(i == 1):
            User_Credentials.name = input("\n> ")
            print("New UserName is " + User_Credentials.name)
        elif(i == 2):
            User_Credentials.password = input("\n> ")
            print("Password changed sucessfully")
        else:
            print("Invalid Input!")

        main()


def login():
    os.system('cls')
    un = input("UserName > ")

    if(os.path.exists("C:\\Users\\Shweta\\Desktop\\UserCredentials\\" + un)):
        p  = input("Password > ")

        UserFile = open("C:\\Users\\Shweta\\Desktop\\UserCredentials\\" + un, "r")
        Content  = UserFile.read()

        password = Content.split()
        if(p == password[0]):
            User_Credentials.login_ = True
            print("Welcome : " + User_Credentials.name)
            main()
        else:
            print("wrong password!\n")
            print("Press 1 - Try Again")
            i = int(input("\n> "))
            if(i == 1):
                login()
            else:
                OnLine()

    else:
        print("Account not found")
        print("Press 1 - Create Account")

    i = int(input("\n> "))
    if(i == 1):
        User_Credentials.new_account()
    else:
        OnLine()

def main():

    os.system('cls')

    if(User_Credentials.login_):
        
        print(
                """
Press 1 - Account status
Press 2 - Withdrawl
Press 3 - Deposit
Press 4 - Manage Account
Press 5 - log_out""")

        j = int(input("\n> "))

        if(j == 1):
            print("Your current Balance is " + str(User_Credentials.current_balance))
            input("")
            main()
        elif(j == 2):
            withdrawl_amount = int(input("> "))
            if(withdrawl_amount <= User_Credentials.current_balance):
                User_Credentials.current_balance -= withdrawl_amount
            else:
                print("Sufficient amount not present!")
            main()
        elif(j == 3):
            add_value = int(input("> ")) 
            User_Credentials.current_balance += add_value
            main()
        elif(j == 4):
            User_Credentials.manage_account()
        elif(j == 5):
            User_Credentials.login_ = False
            os.system('cls')
            OnLine()
        else:
            print("Invalid Input!")

    else:
        login()

def OnLine():
    print("""
Press 1 - Login
Press 2 - New Account
Press 3 - Exit""")

    i = int(input())

    if(i == 1):
        main()
    elif(i ==2 ):
        User_Credentials.new_account()
    elif(i == 3):
        os.system('cls')
        input("<>")
    else:
        print("Invalid Input!")

OnLine()
