<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Food Selling Website</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 0; background-color: #f4f4f4; }
        header { background-color: #ff5722; color: white; text-align: center; padding: 20px; }
        .container { max-width: 1200px; margin: 20px auto; padding: 20px; background: white; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
        .menu { display: flex; flex-wrap: wrap; gap: 20px; }
        .item { border: 1px solid #ddd; padding: 15px; border-radius: 8px; text-align: center; width: 250px; }
        .item img { width: 100%; height: 150px; object-fit: cover; border-radius: 8px; }
        .item h3 { margin: 10px 0; }
        .item p { color: #666; }
        .price { font-weight: bold; color: #ff5722; }
        button { background-color: #ff5722; color: white; border: none; padding: 10px; border-radius: 5px; cursor: pointer; }
        button:hover { background-color: #e64a19; }
        .cart { margin-top: 20px; padding: 20px; background: #f9f9f9; border-radius: 8px; }
        .cart-item { display: flex; justify-content: space-between; margin-bottom: 10px; }
        #total { font-weight: bold; font-size: 18px; }
        form { margin-top: 20px; }
        input, textarea { width: 100%; padding: 10px; margin: 10px 0; border: 1px solid #ddd; border-radius: 5px; }
    </style>
</head>
<body>
    <header>
        <h1>Welcome to Our Food Franchise</h1>
        <p>Order Pizza, Burgers, Pasta & More!</p>
    </header>
    <div class="container">
        <h2>Menu</h2>
        <div class="menu">
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Pizza" alt="Pizza">
                <h3>Margherita Pizza</h3>
                <p>Classic cheese pizza with tomato sauce.</p>
                <p class="price">₹300</p>
                <button onclick="addToCart('Margherita Pizza', 300)">Add to Cart</button>
            </div>
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Burger" alt="Burger">
                <h3>Cheese Burger</h3>
                <p>Juicy burger with cheese and veggies.</p>
                <p class="price">₹250</p>
                <button onclick="addToCart('Cheese Burger', 250)">Add to Cart</button>
            </div>
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Pasta" alt="Pasta">
                <h3>Alfredo Pasta</h3>
                <p>Creamy pasta with chicken and herbs.</p>
                <p class="price">₹400</p>
                <button onclick="addToCart('Alfredo Pasta', 400)">Add to Cart</button>
            </div>
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Fries" alt="Fries">
                <h3>French Fries</h3>
                <p>Crispy golden fries.</p>
                <p class="price">₹100</p>
                <button onclick="addToCart('French Fries', 100)">Add to Cart</button>
            </div>
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Salad" alt="Salad">
                <h3>Caesar Salad</h3>
                <p>Fresh salad with dressing.</p>
                <p class="price">₹200</p>
                <button onclick="addToCart('Caesar Salad', 200)">Add to Cart</button>
            </div>
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Dessert" alt="Dessert">
                <h3>Chocolate Cake</h3>
                <p>Rich chocolate cake slice.</p>
                <p class="price">₹500</p>
                <button onclick="addToCart('Chocolate Cake', 500)">Add to Cart</button>
            </div>
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Drink" alt="Drink">
                <h3>Cold Drink</h3>
                <p>Refreshing soda.</p>
                <p class="price">₹150</p>
                <button onclick="addToCart('Cold Drink', 150)">Add to Cart</button>
            </div>
            <div class="item">
                <img src="https://via.placeholder.com/250x150?text=Combo" alt="Combo">
                <h3>Family Combo</h3>
                <p>Pizza, burger, and fries for 4.</p>
                <p class="price">₹1000</p>
                <button onclick="addToCart('Family Combo', 1000)">Add to Cart</button>
            </div>
        </div>
        
        <div class="cart">
            <h2>Your Cart</h2>
            <div id="cart-items"></div>
            <p id="total">Total: ₹0</p>
            <button onclick="clearCart()">Clear Cart</button>
        </div>
        
        <form id="order-form">
            <h2>Place Order</h2>
            <input type="text" placeholder="MAHASIN ALI" required>
            <input type="email" placeholder="mahasin0465@gmail.com" required>
            <input type="tel" placeholder="88511688835" required>
            <textarea placeholder="gurgaon dlf phase 3 t block new oulet " required></textarea>
            <button type="submit">Submit Order</button>
        </form>
    </div>

    <script>
        let cart = [];
        let total = 0;

        function addToCart(item, price) {
            cart.push({ item, price });
            total += price;
            updateCart();
        }

        function updateCart() {
            const cartItems = document.getElementById('cart-items');
            cartItems.innerHTML = '';
            cart.forEach((item, index) => {
                const div = document.createElement('div');
                div.className = 'cart-item';
                div.innerHTML = `<span>${item.item} - ₹${item.price}</span><button onclick="removeFromCart(${index})">Remove</button>`;
                cartItems.appendChild(div);
            });
            document.getElementById('total').textContent = `Total: ₹${total}`;
        }

        function removeFromCart(index) {
            total -= cart[index].price;
            cart.splice(index, 1);
            updateCart();
        }

        function clearCart() {
            cart = [];
            total = 0;
            updateCart();
        }

        document.getElementById('order-form').addEventListener('submit', function(e) {
            e.preventDefault();
            if (cart.length === 0) {
                alert('Your cart is empty!');
                return;
            }
            alert(`Order placed! Total: ₹${total}. We will contact you soon.`);
            clearCart();
        });
    </script>
</body>
</html>
