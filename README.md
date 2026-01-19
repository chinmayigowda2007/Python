# Python
Assignment
# Product class
class Product:
    def __init__(self, product_id, name, price):
        self.product_id = product_id
        self.name = name
        self.price = price

    def __str__(self):
        return f"{self.name} - ₹{self.price}"


# Cart class
class Cart:
    def __init__(self):
        self.items = {}

    def add_item(self, product, quantity=1):
        if product.product_id in self.items:
            self.items[product.product_id]['quantity'] += quantity
        else:
            self.items[product.product_id] = {'product': product, 'quantity': quantity}
        print(f"Added {quantity} x {product.name} to cart.")

    def remove_item(self, product_id, quantity=1):
        if product_id in self.items:
            if self.items[product_id]['quantity'] > quantity:
                self.items[product_id]['quantity'] -= quantity
                print(f"Removed {quantity} from {self.items[product_id]['product'].name}.")
            else:
                removed_product = self.items.pop(product_id)
                print(f"Removed {removed_product['product'].name} completely from cart.")
        else:
            print("Product not found in cart.")

    def view_cart(self):
        if not self.items:
            print("Cart is empty.")
        else:
            print("\n--- Cart Contents ---")
            for item in self.items.values():
                product = item['product']
                quantity = item['quantity']
                print(f"{product.name} (x{quantity}) - ₹{product.price * quantity}")
            print("---------------------")

    def calculate_total(self):
        total = sum(item['product'].price * item['quantity'] for item in self.items.values())
        print(f"Total Amount: ₹{total}")
        return total


# Example usage
if __name__ == "__main__":
    # Create some products
    p1 = Product(1, "Laptop", 50000)
    p2 = Product(2, "Smartphone", 20000)
    p3 = Product(3, "Headphones", 2000)

    # Create a cart
    cart = Cart()

    # Add items
    cart.add_item(p1, 1)
    cart.add_item(p2, 2)
    cart.add_item(p3, 3)

    # View cart
    cart.view_cart()

    # Remove an item
    cart.remove_item(2, 1)

    # View cart again
    cart.view_cart()

    # Calculate total
    cart.calculate_total()
