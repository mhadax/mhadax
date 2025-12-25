## requst car parkin here 👋

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Arusha City Parking</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f5f5f5;
        text-align: center;
        margin: 0;
        padding: 0;
    }

    header {
        background-color: #4CAF50;
        color: white;
        padding: 20px;
    }

    h1 { margin: 0; }

    .container { padding: 20px; }

    .status {
        font-size: 18px;
        margin: 15px 0;
        font-weight: bold;
    }

    input, select, button {
        padding: 10px;
        margin: 8px 0;
        font-size: 16px;
        width: 270px;
        border-radius: 5px;
        border: 1px solid #ccc;
    }

    button {
        background-color: #4CAF50;
        color: white;
        cursor: pointer;
    }

    button:hover {
        background-color: #45a049;
    }

    footer {
        background-color: #333;
        color: white;
        padding: 15px;
        margin-top: 20px;
    }
</style>
</head>

<body>

<header>
    <h1>Arusha City Parking</h1>
    <p>Request parking and pay online</p>
</header>

<div class="container">

    <div class="status" id="parkingStatus"></div>

    <input type="text" id="name" placeholder="Your Name"><br>

    <input type="text" id="vehicle" placeholder="Plate Number (T123ADF) or Name (frank)"><br>

    <select id="paymentMethod">
        <option value="">Select Payment Method</option>
        <option value="Mpesa">Mpesa</option>
        <option value="HaloPesa">HaloPesa</option>
        <option value="Airtel Money">Airtel Money</option>
        <option value="Mix by YAS">Mix by YAS</option>
    </select><br>

    <button onclick="requestParking()">Request Parking</button>

    <div id="response" class="status"></div>

    <div id="paymentSection" style="display:none;">
        <input type="tel" id="phone" placeholder="Enter Phone Number (07XXXXXXXX)">
        <br>
        <button onclick="makePayment()">Confirm Payment</button>
    </div>

</div>

<footer>
    <p>&copy; 2025 Arusha City Parking</p>
</footer>

<script>
    const maxSpots = 20;
    let availableSpots = maxSpots;
    const pricePerHour = 1000;
    let selectedPayment = "";

    function updateParkingStatus() {
        const status = document.getElementById("parkingStatus");
        if (availableSpots > 0) {
            status.textContent = `Parking Available: ${availableSpots} / ${maxSpots}`;
            status.style.color = "green";
        } else {
            status.textContent = "SORRY, PARKING IS FULL";
            status.style.color = "red";
        }
    }

    function isValidVehicle(input) {
        const platePattern = /^T\d{3}[A-Z]{3}$/; // T123ADF
        const namePattern = /^[a-zA-Z]+$/;       // frank
        return platePattern.test(input.toUpperCase()) || namePattern.test(input);
    }

    function requestParking() {
        const name = document.getElementById("name").value;
        const vehicle = document.getElementById("vehicle").value.trim();
        selectedPayment = document.getElementById("paymentMethod").value;
        const response = document.getElementById("response");

        if (!name || !vehicle || !selectedPayment) {
            response.textContent = "Please fill all fields";
            response.style.color = "orange";
            return;
        }

        if (!isValidVehicle(vehicle)) {
            response.textContent = "Invalid vehicle format. Use T123ADF or name (frank)";
            response.style.color = "red";
            return;
        }

        if (availableSpots > 0) {
            availableSpots--;
            updateParkingStatus();

            response.innerHTML = `
                Parking reserved for <b>${name}</b><br>
                Vehicle ID: <b>${vehicle.toUpperCase()}</b><br>
                Amount: <b>${pricePerHour} TZS</b><br>
                Payment Method: <b>${selectedPayment}</b>
            `;
            response.style.color = "green";

            document.getElementById("paymentSection").style.display = "block";
        } else {
            response.textContent = "SORRY, PARKING IS FULL";
            response.style.color = "red";
        }
    }

    function makePayment() {
        const phone = document.getElementById("phone").value;
        const response = document.getElementById("response");

        if (!phone) {
            alert("Please enter phone number");
            return;
        }

        alert(`Payment request sent to ${phone} via ${selectedPayment}`);

        response.innerHTML = `
            ? Payment Successful!<br>
            Phone: <b>${phone}</b><br>
            Amount Paid: <b>${pricePerHour} TZS</b><br>
            Enjoy your parking.
        `;
        response.style.color = "green";

        document.getElementById("paymentSection").style.display = "none";
    }

    updateParkingStatus();
</script>

</body>
</html>
