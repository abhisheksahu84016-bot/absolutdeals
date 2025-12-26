absolutdeals/
├─ index.html
├─ style.css
├─ app.js
└─ images/
      product1.jpg
      product2.jpg
      product3.jpg
      <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AbsolutDeals</title>
  <link rel="stylesheet" href="style.css">

  <!-- Firebase (optional) -->
  <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.1/firebase-firestore.js"></script>
</head>
<body>
  <header>
    <h1>AbsolutDeals</h1>
    <nav>
      <a href="#">Home</a>
      <a href="#">Cart (<span id="cart-count">0</span>)</a>
    </nav>
  </header>

  <main>
    <section id="products">
      <h2>Our Products</h2>
      <div class="product-list">
        <div class="product">
          <img src="images/product1.jpg" alt="Product 1">
          <h3>Oversized T-Shirt 1</h3>
          <p>₹499</p>
          <button onclick="addToCart('Oversized T-Shirt 1', 499)">Add to Cart</button>
        </div>

        <div class="product">
          <img src="images/product2.jpg" alt="Product 2">
          <h3>Oversized T-Shirt 2</h3>
          <p>₹599</p>
          <button onclick="addToCart('Oversized T-Shirt 2', 599)">Add to Cart</button>
        </div>

        <div class="product">
          <img src="images/product3.jpg" alt="Product 3">
          <h3>Oversized T-Shirt 3</h3>
          <p>₹699</p>
          <button onclick="addToCart('Oversized T-Shirt 3', 699)">Add to Cart</button>
        </div>
      </div>
    </section>

    <section id="cart">
      <h2>Your Cart</h2>
      <ul id="cart-items"></ul>
      <p>Total: ₹<span id="total-price">0</span></p>
      <button onclick="checkout()">Checkout</button>
    </section>
  </main>

  <script src="app.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f5f5f5;
}

header {
  background-color: #ff5733;
  color: white;
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header nav a {
  color: white;
  margin-left: 15px;
  text-decoration: none;
  font-weight: bold;
}

main {
  padding: 20px;
}

.product-list {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.product {
  background-color: white;
  padding: 15px;
  border-radius: 10px;
  width: 200px;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.product img {
  width: 100%;
  border-radius: 10px;
}

button {
  background-color: #ff5733;
  color: white;
  border: none;
  padding: 10px;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background-color: #e64a19;
}
let cart = [];
let totalPrice = 0;

function addToCart(name, price) {
  cart.push({name, price});
  totalPrice += price;
  updateCartUI();
}

function updateCartUI() {
  const cartItems = document.getElementById('cart-items');
  const cartCount = document.getElementById('cart-count');
  const totalPriceEl = document.getElementById('total-price');

  cartItems.innerHTML = '';
  cart.forEach(item => {
    const li = document.createElement('li');
    li.textContent = `${item.name} - ₹${item.price}`;
    cartItems.appendChild(li);
  });

  cartCount.textContent = cart.length;
  totalPriceEl.textContent = totalPrice;
}

function checkout() {
  if(cart.length === 0) {
    alert("Your cart is empty!");
    return;
  }
  alert(`Your order total is ₹${totalPrice}. Checkout functionality can be added later.`);
  cart = [];
  totalPrice = 0;
  updateCartUI();
}
