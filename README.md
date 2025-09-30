<!DOCTYPE html>
<html>
<head>
  <title>Evanshop</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f5f5f5;
    }

    /* Navbar */
    .navbar {
      background: #131921;
      color: white;
      padding: 15px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .navbar h1 {
      margin: 0;
    }
    .nav-buttons button {
      margin-left: 10px;
      background: #febd69;
      border: none;
      padding: 8px 12px;
      border-radius: 5px;
      cursor: pointer;
      font-weight: bold;
    }
    .nav-buttons button:hover {
      background: #f3a847;
    }

    /* Sale Banner */
    .sale-banner {
      background: red;
      color: white;
      text-align: center;
      font-size: 24px;
      font-weight: bold;
      padding: 15px;
      letter-spacing: 2px;
    }

    /* Category Banner */
    .category-banner {
      background: #232f3e;
      color: white;
      padding: 10px;
      font-size: 20px;
      font-weight: bold;
      text-align: left;
    }

    /* Product grid */
    .products {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 20px;
      padding: 20px;
    }

    .product {
      background: white;
      border-radius: 10px;
      padding: 15px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      text-align: center;
      position: relative;
    }
    .product img {
      max-width: 100%;
      height: 150px;
      object-fit: cover;
    }
    .product h3 {
      margin: 10px 0;
    }
    .product button {
      background: #ffd814;
      border: none;
      padding: 10px;
      cursor: pointer;
      border-radius: 5px;
    }
    .product button:hover {
      background: #f7ca00;
    }

    /* Price Styles */
    .price-box { margin: 10px 0; }
    .discount { color: red; font-weight: bold; margin-right: 8px; }
    .sale-price { font-size: 18px; font-weight: bold; color: black; }
    .original-price { text-decoration: line-through; color: gray; font-size: 14px; }

    .sale-badge {
      position: absolute;
      top: 10px;
      left: 10px;
      background: red;
      color: white;
      padding: 5px 10px;
      border-radius: 5px;
      font-size: 14px;
      font-weight: bold;
    }

    /* Sections */
    .section { display: none; padding: 0; }
    .active { display: block; }

    /* Checkout & Returns */
    .checkout-item {
      background: white;
      margin: 10px 0;
      padding: 10px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
    }
    .buy-now {
      margin-top: 20px;
      width: 100%;
      padding: 15px;
      background: green;
      color: white;
      font-size: 18px;
      font-weight: bold;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    .buy-now:hover { background: darkgreen; }

    .summary-box {
      background: #fff;
      padding: 15px;
      margin: 15px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
  </style>
</head>
<body>

  <!-- Navbar -->
  <div class="navbar">
    <h1>Evanshop</h1>
    <div class="nav-buttons">
      <button onclick="showSection('shop')">Shop</button>
      <button onclick="showSection('checkout')">Checkout 🛒</button>
      <button onclick="showSection('returns')">Returns ↩️</button>
    </div>
  </div>

  <!-- SALE Banner -->
  <div class="sale-banner" id="saleBanner">
    HALLOWEEN SALE! September 29th - October 26th
  </div>

  <!-- Shop Section -->
  <div class="section active" id="shop">
    <div class="category-banner">Devices</div>
    <div class="products" id="devices"></div>

    <div class="category-banner">Accessories</div>
    <div class="products" id="accessories"></div>

    <div class="category-banner">Clothing</div>
    <div class="products" id="clothing"></div>

    <div class="category-banner">Shoes</div>
    <div class="products" id="shoes"></div>

    <div class="category-banner">Books</div>
    <div class="products" id="books"></div>

    <div class="category-banner">Toys</div>
    <div class="products" id="toys"></div>

    <div class="category-banner">Home</div>
    <div class="products" id="home"></div>
  </div>

  <!-- Checkout Section -->
  <div class="section" id="checkout">
    <h2>Your Evanshop Cart</h2>
    <div id="cartItems"></div>
    <button class="buy-now" onclick="buyNow()">Buy Now</button>
  </div>

  <!-- Returns Section -->
  <div class="section" id="returns">
    <h2>Return Items</h2>
    <div id="returnItems"></div>
  </div>

  <!-- Spent Tracker -->
  <div class="summary-box">
    <h3>Total Spent: $<span id="spentAmount">0.00</span></h3>
  </div>

  <script>
    // Categories
    const devices = [
      { name: "Laptop", price: 999, discountPercent: 20, img: "https://via.placeholder.com/200" },
      { name: "Phone", price: 699, discountPercent: 15, img: "https://via.placeholder.com/200" },
      { name: "Tablet", price: 799, discountPercent: 25, img: "https://via.placeholder.com/200" }
    ];
    const accessories = [
      { name: "Headphones", price: 199, discountPercent: 0, img: "https://via.placeholder.com/200" },
      { name: "Smartwatch", price: 299, discountPercent: 20, img: "https://via.placeholder.com/200" }
    ];
    const clothing = [
      { name: "T-Shirt", price: 25, discountPercent: 10, img: "https://via.placeholder.com/200" },
      { name: "Shorts", price: 13, discountPercent: 5, img: "https://via.placeholder.com/200" },
    ];
    const shoes = [
      { name: " Nike sneakers", price: 89, discountPercent: 5, img: "https://via.placeholder.com/200" },
      { name: "Puma sneakers", price: 120, discountPercent: 20, img: "https://via.placeholder.com/200" },
      { name: "Crocs", price: 30, discountPercent: 0, img: "https://via.placeholder.com/200" }
    ];
    const books = [
      { name: "Dog man", price: 19, discountPercent: 0, img: "https://via.placeholder.com/200" },
      { name: "Diary of a wimpy kid", price: 16, discountPercent: 50, img: "https://via.placeholder.com/200" }
    ];
    const toys = [
      { name: "Lego Set", price: 75, discountPercent: 18, img: "https://via.placeholder.com/200" },
      { name: "Hotwheels Tesla", price: 18, discountPercent: 2, img: "https://via.placeholder.com/200" }
    ];
    const home = [
      { name: "Lamp", price: 45, discountPercent: 0, img: "https://via.placeholder.com/200" },
      { name: "Matress", price: 139, discountPercent: 5, img: "https://via.placeholder.com/200" }
    ];

    let cart = [];
    let pastPurchases = [];
    let totalSpent = 0;

    const spentAmountEl = document.getElementById("spentAmount");
    const returnItemsDiv = document.getElementById("returnItems");
    const cartItemsDiv = document.getElementById("cartItems");

    function calculateSalePrice(price, discountPercent) {
      return (price - (price * discountPercent / 100)).toFixed(2);
    }

    function renderProducts(list, containerId) {
      const container = document.getElementById(containerId);
      list.forEach(p => {
        const div = document.createElement("div");
        div.classList.add("product");
        const finalPrice = p.discountPercent > 0 ? calculateSalePrice(p.price, p.discountPercent) : p.price;
        div.innerHTML = `
          ${p.discountPercent > 0 ? `<div class="sale-badge">-${p.discountPercent}%</div>` : ""}
          <img src="${p.img}" alt="${p.name}">
          <h3>${p.name}</h3>
          ${p.discountPercent > 0 
            ? `<div class="price-box"><span class="discount">-${p.discountPercent}%</span>
               <span class="sale-price">$${finalPrice}</span><br>
               <span class="original-price">List Price: $${p.price}</span></div>`
            : `<p>$${p.price}</p>`}
          <button>Add to Cart</button>
        `;
        div.querySelector("button").addEventListener("click", () => {
          cart.push({ ...p, finalPrice: parseFloat(finalPrice) });
          alert(`${p.name} added to your Evanshop cart!`);
        });
        container.appendChild(div);
      });
    }

    // Render all categories
    renderProducts(devices, "devices");
    renderProducts(accessories, "accessories");
    renderProducts(clothing, "clothing");
    renderProducts(shoes, "shoes");
    renderProducts(books, "books");
    renderProducts(toys, "toys");
    renderProducts(home, "home");

    function showSection(id) {
      document.querySelectorAll(".section").forEach(s => s.classList.remove("active"));
      document.getElementById(id).classList.add("active");
      if (id === "checkout") renderCart();
      if (id === "returns") renderReturns();
    }

    function renderCart() {
      cartItemsDiv.innerHTML = "";
      if (cart.length === 0) {
        cartItemsDiv.innerHTML = "<p>Your cart is empty.</p>";
        return;
      }
      cart.forEach(item => {
        const div = document.createElement("div");
        div.classList.add("checkout-item");
        div.innerHTML = `<span>${item.name}</span> <span>$${item.finalPrice}</span>`;
        cartItemsDiv.appendChild(div);
      });
    }

    function buyNow() {
      if (cart.length === 0) {
        alert("Your Evanshop cart is empty!");
        return;
      }
      cart.forEach(item => {
        pastPurchases.push(item);
        totalSpent += item.finalPrice;
      });
      spentAmountEl.textContent = totalSpent.toFixed(2);
      alert("Thank you for shopping at Evanshop!");
      cart = [];
      renderCart();
    }

    function renderReturns() {
      returnItemsDiv.innerHTML = "";
      if (pastPurchases.length === 0) {
        returnItemsDiv.innerHTML = "<p>No items available for return.</p>";
        return;
      }
      pastPurchases.forEach((item, index) => {
        const div = document.createElement("div");
        div.classList.add("checkout-item");
        div.innerHTML = `<span>${item.name} - $${item.finalPrice}</span>
                         <button onclick="returnItem(${index})">Return</button>`;
        returnItemsDiv.appendChild(div);
      });
    }

    function returnItem(index) {
      const item = pastPurchases[index];
      totalSpent -= item.finalPrice;
      spentAmountEl.textContent = totalSpent.toFixed(2);
      pastPurchases.splice(index, 1);
      renderReturns();
      alert(`${item.name} has been returned. $${item.finalPrice} refunded!`);
    }
  </script>

</body>
</html>
