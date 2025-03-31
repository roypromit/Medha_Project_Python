# Medha_Project_Python
def add_expense(expenses): #adding expenses fuction
        date=input('Enter date in format YYYY-MM-DD: ')
        catagory=input('Enter catagory such as Food, Travel, etc: ')
        amount=float(input('Enter the amount spent: '))
        description=input('Enter a description: ')
    
        exp={'date':date,'category':catagory, 'amount':amount, 'description':description}
        expenses.append(exp)
        print("Expenses added Successfully!!")
        
    
    def view_expenses(expenses): #displaying the expenses
        if not expenses:
            print("No expenses recorded yet. \n")
    
        print('Expenses List:')
        print("Date   | Catagory   | Amount   | Description  ")
        print('-'*50)
        for expenses in expenses:
            print(f"{expenses['date']}   | {expenses['category']}   | ${expenses['amount']:.2f}   | {expenses['description']}")
            print("\n")
    
    def set_budget():
        return float(input("Enter your monthly budget: "))
    
    def track_budget(expenses,budget):
        total_spent=sum(exp['amount'] for exp in expenses)
        print(f"Total spent : ${total_spent:.2f}")
        if total_spent>budget:
            print("Warning you have exceeded budget.\n")
        else:
            print(f"Remaining Budget: ${budget-total_spent:.2f}\n")
    def save_expenses(expenses): #create test.csv file in location
        import pandas as pd
        df=pd.DataFrame(expenses)
        df.to_csv("test.csv", index=False)
        print('Entry saved successfully!')    
    
    def load_expense(expenses):
        from csv import DictReader
        with open("test.csv","r") as f:
                dict_reader=DictReader(f)
                reader=list(dict_reader)
                if bool(reader)==True: 
                    for row in reader:
                        expenses.append(dict(row))
                else:
                    print('file is empty')
                for expense in expenses:
                    expense['amount'] = float(expense['amount'])
        print("Expense loaded successfully")
            
    def main():
        expenses = []
        budget = set_budget()
    
        while True:
            print("\n Personal Expense Tracker")
            print("0. Load previous expenses")
            print("1. Add Expense")
            print("2. View Expense")
            print("3. Track Expense")
            print("4. Save")
            print("5. Exit")
            choice=input("choose the options from above: ")
            
            if choice == "0":
                load_expense(expenses)
            elif choice == "1":
                add_expense(expenses)
            elif choice == "2":
                view_expenses(expenses)
            elif choice == "3":
                track_budget(expenses,budget)
            elif choice == "4":
                save_expenses(expenses)
            elif choice == "5":
                print("Exiting...\n")
                break
            else:
                print("Invalid Choice or data, pls try again \n")
    
    if __name__=="__main__":
        main()
