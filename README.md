<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Merry Christmas</title>

<style>
    body {
        background-color: #f2f2f2;
        font-family: Arial, sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }

    .card {
        background-color: #1565c0; /* Blue rectangle */
        color: white;
        padding: 40px 60px;
        text-align: center;
        border-radius: 8px;
        box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        max-width: 600px;
    }

    .card h1 {
        font-size: 50px;
        margin: 0 0 15px 0;
    }

    .card p {
        font-size: 22px;
        margin: 8px 0;
    }

    .highlight {
        margin-top: 20px;
        font-size: 24px;
        font-weight: bold;
        color: #ffeb3b;
    }
</style>
</head>

<body>

<div class="card">
    <h1>🎄 Merry Christmas 🎄</h1>
    <p>Wishing you peace, joy, and happiness</p>
    <p><strong>— by Mhadax.com</strong></p>

    <p class="highlight">WAKUU TUNA NGOJA MIALIKO</p>
</div>

</body>
</html>

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
👋

