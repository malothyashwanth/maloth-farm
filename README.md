<!-- Add this inside your product section or in a new <section> -->
<section id="order-form">
    <h3>Place Your Order (Today: 0/100 orders)</h3>
    <form id="orderForm">
        <label>Name: <input type="text" required></label><br>
        <label>Phone: <input type="text" required></label><br>
        <label>Address: <input type="text" required></label><br>
        <label>Product: 
            <select required>
                <option value="Paddy">Paddy (₹50/kg)</option>
                <option value="Milk">Cow Milk (₹60/L)</option>
                <option value="Pulses">Pulses (₹100/kg)</option>
            </select>
        </label><br>
        <label>Quantity: <input type="number" min="1" required></label><br>
        <button type="submit" id="orderBtn">Submit Order</button>
    </form>
    <p id="status"></p>
</section>

<script>
// TODAY’s date key (simple day limit)
let today = new Date().toDateString();
let orderCountKey = "orders_" + today;

// Load today’s count from localStorage
let count = localStorage.getItem(orderCountKey) || 0;
count = parseInt(count);

// Update text
document.querySelector("h3").innerHTML = 
    `Place Your Order (Today: ${count}/100 orders)`;

document.getElementById("orderForm").addEventListener("submit", function(e) {
    e.preventDefault();
    if (count >= 100) {
        document.getElementById("status").innerHTML = 
            "⚠ Daily limit of 100 orders reached. Please order tomorrow.";
        return;
    }
    
    // Just show success on the page (you can also send to Google Form / WhatsApp)
    document.getElementById("status").innerHTML = 
        "✅ Order placed! We will call you soon.";
    
    // Increase and save count
    count += 1;
    localStorage.setItem(orderCountKey, count);
});
</script>
