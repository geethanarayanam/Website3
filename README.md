<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vastramanjiri6 | Luxury Sarees</title>
    <style>
        :root { --maroon: #800000; --gold: #d4af37; }
        body { margin: 0; font-family: 'Playfair Display', serif; background: #fffaf0; }
        header { background: var(--maroon); color: var(--gold); padding: 25px; text-align: center; position: sticky; top: 0; z-index: 100; }
        
        .container { padding: 20px; max-width: 1200px; margin: auto; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 25px; }
        
        /* Product Cards */
        .card { background: white; padding: 15px; border-radius: 15px; border: 1px solid var(--gold); text-align: center; transition: 0.3s; }
        .card:hover { transform: translateY(-5px); box-shadow: 0 10px 20px rgba(0,0,0,0.1); }
        .card img { width: 100%; height: 350px; object-fit: cover; border-radius: 10px; }
        
        /* Quantity Counter */
        .qty-box { display: flex; align-items: center; justify-content: center; gap: 15px; margin: 15px 0; }
        .q-btn { background: var(--maroon); color: white; border: none; width: 30px; height: 30px; border-radius: 50%; cursor: pointer; font-size: 1.2rem; }
        .q-val { font-weight: bold; font-size: 1.1rem; }

        .order-now { background: var(--maroon); color: white; border: none; padding: 12px; width: 100%; border-radius: 8px; font-weight: bold; cursor: pointer; font-size: 1rem; }

        /* Payment Modal */
        #payment-modal { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.9); justify-content:center; align-items:center; z-index:1000; }
        .modal-box { background: white; padding: 30px; border-radius: 20px; width: 90%; max-width: 400px; text-align: center; }
        .insta-btn { background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888); color: white; border: none; padding: 15px; width: 100%; border-radius: 10px; font-weight: bold; cursor: pointer; margin-top: 15px; }
    </style>
</head>
<body>

<header>
    <h1>VASTRAMANJIRI</h1>
    <p>Handpicked Elegance for You</p>
</header>

<div class="container">
    <div class="grid" id="saree-grid">
        </div>
</div>

<div id="payment-modal">
    <div class="modal-box">
        <h2 style="color:var(--maroon)">Scan to Pay</h2>
        <div id="order-info" style="margin-bottom: 20px; border-bottom: 1px solid #eee; padding-bottom: 15px;"></div>
        <img src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=upi://pay?pa=YOUR_UPI_ID@okicici" alt="QR Code">
        <p>UPI ID: yourname@bank</p>
        <button class="insta-btn" onclick="notifyInstagram()">PAY & DM ORDER TO INSTAGRAM</button>
        <button onclick="document.getElementById('payment-modal').style.display='none'" style="border:none; background:none; color:grey; margin-top:15px; cursor:pointer;">Cancel</button>
    </div>
</div>

<script>
    // 1. THE 100 SAREE LIST (Add all 100 here)
    const sarees = [
        { name: "Banarasi Silk Saree", price: 4500, img: "https://via.placeholder.com/300x400?text=Saree+1" },
        { name: "Kanchipuram Red", price: 6200, img: "https://via.placeholder.com/300x400?text=Saree+2" },
        { name: "Chiffon Embroidered", price: 3500, img: "https://via.placeholder.com/300x400?text=Saree+3" },
        // To reach 100, just copy and paste the line above!
    ];

    const grid = document.getElementById('saree-grid');
    let currentOrder = {};

    // 2. THE LOOP: This builds the cards automatically
    sarees.forEach((s, index) => {
        grid.innerHTML += `
            <div class="card">
                <img src="${s.img}" alt="${s.name}">
                <h3>${s.name}</h3>
                <p style="color:var(--maroon); font-weight:bold; font-size:1.2rem;">₹${s.price}</p>
                <div class="qty-box">
                    <button class="q-btn" onclick="updateQty(${index}, -1)">-</button>
                    <span class="q-val" id="qty-${index}">1</span>
                    <button class="q-btn" onclick="updateQty(${index}, 1)">+</button>
                </div>
                <button class="order-now" onclick="openPayment(${index})">ORDER NOW</button>
            </div>
        `;
    });

    function updateQty(index, change) {
        let el = document.getElementById(`qty-${index}`);
        let val = parseInt(el.innerText);
        if(val + change >= 1) el.innerText = val + change;
    }

    function openPayment(index) {
        let qty = document.getElementById(`qty-${index}`).innerText;
        let item = sarees[index];
        currentOrder = { name: item.name, qty: qty, total: item.price * qty };

        document.getElementById('order-info').innerHTML = `
            <h3>${currentOrder.name}</h3>
            <p>Qty: ${currentOrder.qty} | Total: ₹${currentOrder.total}</p>
        `;
        document.getElementById('payment-modal').style.display = 'flex';
    }

    function notifyInstagram() {
        const username = "Vastramanjiri6"; 
        const msg = `New Order Details:%0AItem: ${currentOrder.name}%0AQuantity: ${currentOrder.qty}%0ATotal: ₹${currentOrder.total}%0A%0AI have scanned the QR. Please confirm!`;
        
        // This link opens the Instagram DM composer
        window.open(`https://www.instagram.com/direct/t/${username}/?text=${msg}`, '_blank');
        
        // Safety Fallback to profile
        setTimeout(() => {
            window.location.href = `https://instagram.com/${username}`;
        }, 1500);
    }
</script>
</body>
</html>
