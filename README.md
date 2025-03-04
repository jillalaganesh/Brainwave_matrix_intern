# Brainwave_matrox_intern
class ATM:
    def __init__(self):
        # Initialize with a sample account data (you can replace it with a database or file)
        self.accounts = {
            "123456": {"pin": "1234", "balance": 1000.0},  # Account number : pin, balance
            "987654": {"pin": "4321", "balance": 5000.0},
        }
        self.current_account = None

    def authenticate_user(self):
        print("Welcome to the ATM!")
        account_number = input("Please enter your account number: ")
        if account_number in self.accounts:
            pin = input("Please enter your PIN: ")
            if pin == self.accounts[account_number]["pin"]:
                self.current_account = account_number
                print("Authentication successful!")
                return True
            else:
                print("Invalid PIN.")
        else:
            print("Account not found.")
        return False

    def show_balance(self):
        balance = self.accounts[self.current_account]["balance"]
        print(f"Your current balance is: ${balance:.2f}")

    def deposit(self):
        try:
            amount = float(input("Enter the amount to deposit: $"))
            if amount > 0:
                self.accounts[self.current_account]["balance"] += amount
                print(f"Successfully deposited ${amount:.2f}")
            else:
                print("Amount should be positive.")
        except ValueError:
            print("Invalid input. Please enter a valid number.")

    def withdraw(self):
        try:
            amount = float(input("Enter the amount to withdraw: $"))
            if amount > 0:
                balance = self.accounts[self.current_account]["balance"]
                if amount <= balance:
                    self.accounts[self.current_account]["balance"] -= amount
                    print(f"Successfully withdrew ${amount:.2f}")
                else:
                    print("Insufficient balance.")
            else:
                print("Amount should be positive.")
        except ValueError:
            print("Invalid input. Please enter a valid number.")

    def logout(self):
        print("Thank you for using the ATM. Goodbye!")
        self.current_account = None

    def menu(self):
        while True:
            print("\nATM Menu:")
            print("1. View Balance")
            print("2. Deposit")
            print("3. Withdraw")
            print("4. Logout")
            try:
                choice = int(input("Please select an option (1-4): "))
                if choice == 1:
                    self.show_balance()
                elif choice == 2:
                    self.deposit()
                elif choice == 3:
                    self.withdraw()
                elif choice == 4:
                    self.logout()
                    break
                else:
                    print("Invalid choice. Please select a valid option.")
            except ValueError:
                print("Invalid input. Please enter a valid number.")

def main():
    atm = ATM()
    while not atm.authenticate_user():
        print("Please try again.")
    atm.menu()

if __name__ == "__main__":
    main()
