# Expense_tracker.py
import json

# File name
file_name = "expenses.json"

# Load old data if file exists
def load_expenses():
    try:
        with open(file_name, "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return []

# Save data to JSON file
def save_expenses(expenses):
    with open(file_name, "w") as file:
        json.dump(expenses, file, indent=4)

# Add new expense
def add_expense(name, amount):
    expenses = load_expenses()
    expenses.append({"name": name, "amount": amount})
    save_expenses(expenses)
    print(f"Added {name} - ₹{amount}")

# Show all expenses
def show_expenses():
    expenses = load_expenses()
    total = sum(item["amount"] for item in expenses)
    print("\nYour Expenses:")
    for item in expenses:
        print(f"{item['name']} - ₹{item['amount']}")
    print(f"\nTotal = ₹{total}")

# Main
while True:
    print("\n1. Add Expense\n2. Show Expenses\n3. Exit")
    choice = input("Enter choice: ")

    if choice == "1":
        name = input("Enter expense name: ")
        amount = int(input("Enter amount: "))
        add_expense(name, amount)
    elif choice == "2":
        show_expenses()
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid choice, try again.")
