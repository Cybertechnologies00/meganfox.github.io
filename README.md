<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Subscribe to MEGAN FOX</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #fdfdfd;
      padding: 20px;
      max-width: 500px;
      margin: auto;
    }
    h1 {
      text-align: center;
    }
    .channel-info {
      background-color: #f0f0f0;
      padding: 15px;
      border-radius: 8px;
      margin-bottom: 20px;
    }
    label, input, select {
      display: block;
      width: 100%;
      margin-bottom: 15px;
      font-size: 16px;
    }
    button {
      background-color: #333;
      color: white;
      padding: 12px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background-color: #444;
    }
    .message {
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>Subscribe to MEGAN FOX</h1>
  <div class="channel-info">
    <p><strong>Channel:</strong> MEGAN FOX</p>
    <p><strong>Subscribers:</strong> 52.7M</p>
    <p><strong>Price:</strong> $20.00</p>
  </div>

  <form id="subscriptionForm">
    <label for="email">Email Address:</label>
    <input type="email" id="email" required>

    <label for="paymentMethod">Payment Method:</label>
    <select id="paymentMethod" required>
      <option value="">-- Select --</option>
      <option value="giftcard">🎁 Gift Card</option>
      <option value="bitcoin">₿ Bitcoin</option>
    </select>

    <div id="giftCardInput" style="display:none;">
      <label for="giftCardCode">Gift Card Code:</label>
      <input type="text" id="giftCardCode">
    </div>

    <div id="bitcoinInput" style="display:none;">
      <label for="bitcoinTxHash">Bitcoin Transaction Hash:</label>
      <input type="text" id="bitcoinTxHash">
    </div>

    <button type="submit">Subscribe</button>
  </form>

  <div class="message" id="message"></div>

  <script>
    const form = document.getElementById('subscriptionForm');
    const paymentMethod = document.getElementById('paymentMethod');
    const giftCardInput = document.getElementById('giftCardInput');
    const bitcoinInput = document.getElementById('bitcoinInput');
    const messageBox = document.getElementById('message');

    paymentMethod.addEventListener('change', () => {
      giftCardInput.style.display = paymentMethod.value === 'giftcard' ? 'block' : 'none';
      bitcoinInput.style.display = paymentMethod.value === 'bitcoin' ? 'block' : 'none';
    });

    form.addEventListener('submit', async (e) => {
      e.preventDefault();

      const email = document.getElementById('email').value;
      const method = paymentMethod.value;
      const giftCardCode = document.getElementById('giftCardCode').value;
      const bitcoinTxHash = document.getElementById('bitcoinTxHash').value;

      const payload = {
        email,
        paymentMethod: method,
      };

      if (method === 'giftcard') {
        payload.giftCardCode = giftCardCode;
      } else if (method === 'bitcoin') {
        payload.bitcoinTxHash = bitcoinTxHash;
      }

      try {
        const response = await fetch('http://localhost:3000/subscribe', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(payload),
        });

        const result = await response.json();

        if (response.ok) {
          messageBox.textContent = result.message;
          messageBox.style.color = 'green';
        } else {
          messageBox.textContent = result.error || 'Something went wrong.';
          messageBox.style.color = 'red';
        }
      } catch (err) {
        messageBox.textContent = 'Server error. Please try again later.';
        messageBox.style.color = 'red';
      }
    });
  </script>
</body>
</html>
/* Global Styles */
body {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-image: url('https://images.unsplash.com/photo-1542204165-65bf26472b9b?auto=format&fit=crop&w=1400&q=80');
  background-size: cover;
  background-position: center;
  color: #fff;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Overlay for better readability */
body::before {
  content: '';
  position: absolute;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.6);
  z-index: -1;
}

/* Main Container */
.container {
  background-color: rgba(30, 30, 30, 0.9);
  padding: 30px;
  border-radius: 12px;
  width: 100%;
  max-width: 5
