<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Branded Receipt Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f8f9fa;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 100%;
            max-width: 600px;
            margin: 20px auto;
            padding: 20px;
            border-radius: 10px;
            background-color: white;
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
        }
        .receipt {
            display: none;
            text-align: left;
            background-color: white;
            border-radius: 10px;
            width: 100%;
            max-width: 600px;
            padding: 20px;
            margin: 20px auto;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .brand-logo, .product-image {
            width: 100px;
            height: auto;
        }
        button {
            margin-top: 10px;
            padding: 10px;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        .gmail-container {
            background-color: #fff;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-family: 'Arial', sans-serif;
            font-size: 14px;
            color: #333;
        }
        .gmail-header {
            font-weight: bold;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <h2>Branded Receipt Generator</h2>
    <div class="container">
        <label>Select a Brand:
            <select id="brand">
                <option value="Nike">Nike</option>
                <option value="Apple">Apple</option>
                <option value="Walmart">Walmart</option>
                <option value="Starbucks">Starbucks</option>
            </select>
        </label>
        <br><br>
        <label>Customer Name: <input type="text" id="customer"></label><br><br>
        <label>Email: <input type="email" id="email"></label><br><br>
        <label>Shipping Address: <input type="text" id="address"></label><br><br>
        <label>Item: <input type="text" id="item"></label><br><br>
        <label>Price: <input type="number" id="price"></label><br><br>
        <label>Product Image URL: <input type="text" id="productImage"></label><br><br>
        <button onclick="generateReceipt()">Generate Receipt</button>
    </div>
    <div id="receipt" class="receipt gmail-container">
        <div class="gmail-header">Purchase Confirmation</div>
        <h3 id="brandTitle"></h3>
        <img id="brandLogo" class="brand-logo" src="" alt="Brand Logo"><br><br>
        <img id="productImg" class="product-image" src="" alt="Product Image"><br><br>
        <p id="receiptDetails"></p>
        <button onclick="window.print()">Print</button>
    </div>
    <script>
        const brandDetails = {
            "Nike": { logo: "https://upload.wikimedia.org/wikipedia/commons/a/a6/Logo_NIKE.svg", email: "order@nike.com" },
            "Apple": { logo: "https://upload.wikimedia.org/wikipedia/commons/f/fa/Apple_logo_black.svg", email: "store@apple.com" },
            "Walmart": { logo: "https://upload.wikimedia.org/wikipedia/commons/c/ca/Walmart_logo.svg", email: "support@walmart.com" },
            "Starbucks": { logo: "https://upload.wikimedia.org/wikipedia/en/4/45/Starbucks_Corporation_Logo_2011.svg", email: "orders@starbucks.com" }
        };

        function generateReceipt() {
            const brand = document.getElementById("brand").value;
            const customer = document.getElementById("customer").value;
            const email = document.getElementById("email").value;
            const address = document.getElementById("address").value;
            const item = document.getElementById("item").value;
            const price = document.getElementById("price").value;
            const productImage = document.getElementById("productImage").value;
            const trackingNumber = "TRK" + Math.floor(Math.random() * 1000000);
            const deliveryDate = new Date();
            deliveryDate.setDate(deliveryDate.getDate() + 5);
            const brandData = brandDetails[brand];
            document.getElementById("brandTitle").innerText = `${brand} Purchase Confirmation`;
            document.getElementById("brandLogo").src = brandData.logo;
            document.getElementById("productImg").src = productImage;
            document.getElementById("receiptDetails").innerHTML = `
                <strong>From:</strong> ${brandData.email} <br>
                <strong>To:</strong> ${email} <br><br>
                Dear ${customer}, <br><br>
                Thank you for your order! Your purchase has been confirmed. <br><br>
                <strong>Order Details:</strong><br>
                Item: ${item} <br>
                Price: $${price} <br>
                Tracking Number: ${trackingNumber} <br>
                Estimated Delivery: ${deliveryDate.toDateString()} <br><br>
                Thank you for shopping at ${brand}!`;
            document.getElementById("receipt").style.display = "block";
        }
    </script>
</body>
</html>
