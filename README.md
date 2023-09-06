class Expense:
    def __init__(self, category, description, amount, date):
        self.category = category
        self.description = description
        self.amount = amount
        self.date = date

class ExpenseTracker:
    def __init__(self):
        self.expenses = []

    def add_expense(self, expense):
        self.expenses.append(expense)

    def calculate_total_expenses(self):
        total = sum(expense.amount for expense in self.expenses)
        return total

    def view_expenses_by_category(self, category):
        category_expenses = [expense for expense in self.expenses if expense.category == category]
        return category_expenses

    def generate_spending_report(self):
        report = {}
        for expense in self.expenses:
            if expense.category in report:
                report[expense.category] += expense.amount
            else:
                report[expense.category] = expense.amount
        return report

if __name__ == "__main__":
    expense_tracker = ExpenseTracker()

    while True:
        print("\nExpense Tracker")
        print("1. Add Expense")
        print("2. Calculate Total Expenses")
        print("3. View Expenses by Category")
        print("4. Generate Spending Report")
        print("5. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            category = input("Enter expense category: ")
            description = input("Enter expense description: ")
            amount = float(input("Enter expense amount: "))
            date = input("Enter expense date (yyyy-mm-dd): ")
            expense = Expense(category, description, amount, date)
            expense_tracker.add_expense(expense)
        elif choice == "2":
            total_expenses = expense_tracker.calculate_total_expenses()
            print(f"Total Expenses: ${total_expenses:.2f}")
        elif choice == "3":
            category = input("Enter category to view expenses: ")
            category_expenses = expense_tracker.view_expenses_by_category(category)
            for expense in category_expenses:
                print(f"Category: {expense.category}, Description: {expense.description}, Amount: ${expense.amount:.2f}")
        elif choice == "4":
            spending_report = expense_tracker.generate_spending_report()
            for category, amount in spending_report.items():
                print(f"Category: {category}, Total Expenses: ${amount:.2f}")
        elif choice == "5":
            break
        else:
            print("Invalid choice. Please try again.")

