# Friendie-Cup-Order-Management-System-
# COFFEE SHOP ORDER MANAGEMENT SYSTEM
# C.O.F.F.E.E.
# Christ Offers Forgiveness For Everyone Everywhere

menu = {
    1: ("Strawberry Yogurt Cream Milk", 38),
    2: ("Choco Lava", 38),
    3: ("Taro Cream Milk", 38),
    4: ("Caramel Latte", 38),
    5: ("Mocha Caramel", 38),
    6: ("Mocha Latte", 38)
}

orders = []
order_number = 1


# DISPLAY MENU
def show_menu():
    print("\n==========================================")
    print("              C.O.F.F.E.E.")
    print("==========================================")
    print("                 MENU")
    print("------------------------------------------")

    for number, item in menu.items():
        print(f"{number}. {item[0]} - PHP {item[1]:.2f}")

    print("==========================================")


# ADD NEW ORDER
def add_order():
    global order_number

    customer = input("\nEnter customer name: ")

    items = []
    total = 0

    while True:
        show_menu()
        print("0. Finish Order")

        try:
            choice = int(input("\nChoose a drink: "))

            if choice == 0:
                break

            if choice not in menu:
                print("Invalid menu choice. Please try again.")
                continue

            quantity = int(input("Enter quantity: "))

            if quantity <= 0:
                print("Quantity must be greater than zero.")
                continue

            name, price = menu[choice]
            subtotal = price * quantity
            total += subtotal

            items.append({
                "name": name,
                "quantity": quantity,
                "price": price,
                "subtotal": subtotal
            })

            print(f"{quantity} x {name} added successfully!")
            print(f"Subtotal: PHP {subtotal:.2f}")

        except ValueError:
            print("Invalid input. Please enter a number.")

    if len(items) == 0:
        print("No items ordered. Order not saved.")
        return

    order = {
        "number": order_number,
        "customer": customer,
        "items": items,
        "total": total,
        "status": "Pending"
    }

    orders.append(order)

    print("\n========== ORDER SUMMARY ==========")
    print("Order Number:", order_number)
    print("Customer:", customer)
    print("-----------------------------------")

    for item in items:
        print(
            f"{item['name']} x {item['quantity']} "
            f"= PHP {item['subtotal']:.2f}"
        )

    print("-----------------------------------")
    print(f"TOTAL: PHP {total:.2f}")
    print("Order Status: Pending")
    print("===================================")

    order_number += 1


# VIEW ALL ORDERS
def view_orders():
    print("\n========== ALL CUSTOMER ORDERS ==========")

    if len(orders) == 0:
        print("No orders available.")
        return

    for order in orders:
        print("\nOrder Number:", order["number"])
        print("Customer:", order["customer"])
        print("-----------------------------------------")

        for item in order["items"]:
            print(
                f"{item['name']} x {item['quantity']} "
                f"= PHP {item['subtotal']:.2f}"
            )

        print(f"Total: PHP {order['total']:.2f}")
        print("Status:", order["status"])
        print("-----------------------------------------")


# UPDATE ORDER STATUS
def update_status():
    if len(orders) == 0:
        print("\nNo orders available to update.")
        return

    view_orders()

    try:
        number = int(input("\nEnter order number to update: "))

        for order in orders:
            if order["number"] == number:

                print("\nChoose New Order Status:")
                print("1. Pending")
                print("2. Preparing")
                print("3. Completed")

                choice = input("Enter your choice: ")

                if choice == "1":
                    order["status"] = "Pending"

                elif choice == "2":
                    order["status"] = "Preparing"

                elif choice == "3":
                    order["status"] = "Completed"

                else:
                    print("Invalid status choice.")
                    return

                print("\nOrder status updated successfully!")
                print("New Status:", order["status"])
                return

        print("Order number not found.")

    except ValueError:
        print("Please enter a valid order number.")


# MAIN PROGRAM
while True:
    print("\n==========================================")
    print("              C.O.F.F.E.E.")
    print("==========================================")
    print("1. Display Menu")
    print("2. Add New Order")
    print("3. View All Orders")
    print("4. Update Order Status")
    print("5. Exit")
    print("==========================================")

    choice = input("Choose an option (1-5): ")

    if choice == "1":
        show_menu()

    elif choice == "2":
        add_order()

    elif choice == "3":
        view_orders()

    elif choice == "4":
        update_status()

    elif choice == "5":
        print("\nThank you for using C.O.F.F.E.E.!")
        print("Have a great day!")
        break

    else:
        print("Invalid choice. Please select from 1 to 5.")

