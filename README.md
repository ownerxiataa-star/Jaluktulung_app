# Jaluktulung_app
Aplikasi jasa pengiriman dll
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jaluk Tulung - Star App</title>
    <!-- Menggunakan Font Awesome untuk Ikon -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root {
            --primary: #00b894; /* Hijau Jaluk Tulung */
            --secondary: #0984e3;
            --dark: #2d3436;
            --light: #f5f6fa;
            --white: #ffffff;
            --shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }
        
        body { background-color: var(--light); color: var(--dark); padding-bottom: 70px; }

        /* HEADER */
        header {
            background: linear-gradient(135deg, var(--primary), #00cec9);
            padding: 20px;
            color: white;
            border-bottom-left-radius: 20px;
            border-bottom-right-radius: 20px;
            box-shadow: var(--shadow);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }
        .logo { font-size: 24px; font-weight: bold; letter-spacing: 1px; }
        .location { font-size: 14px; opacity: 0.9; }
        .location i { margin-right: 5px; }

        /* MENU GRID */
        .menu-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            padding: 20px;
            margin-top: -30px;
            background: transparent;
        }

        .menu-item {
            background: white;
            padding: 15px 5px;
            border-radius: 15px;
            text-align: center;
            box-shadow: var(--shadow);
            cursor: pointer;
            transition: transform 0.2s;
        }

        .menu-item:active { transform: scale(0.95); }
        .menu-icon { font-size: 24px; color: var(--primary); margin-bottom: 8px; }
        .menu-text { font-size: 12px; font-weight: 600; }

        /* SECTIONS */
        .section-title { padding: 0 20px; margin: 20px 0 10px; font-size: 18px; font-weight: bold; }
        
        /* FOOD LIST */
        .food-container {
            display: flex;
            overflow-x: auto;
            padding: 10px 20px;
            gap: 15px;
            scrollbar-width: none;
        }
        
        .food-card {
            min-width: 160px;
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: var(--shadow);
        }

        .food-img { height: 100px; background: #ddd; display: flex; align-items: center; justify-content: center; color: #888; }
        .food-info { padding: 10px; }
        .food-name { font-size: 14px; font-weight: bold; margin-bottom: 5px; }
        .food-price { color: var(--primary); font-weight: bold; font-size: 13px; }
        .btn-add { 
            width: 100%; margin-top: 8px; padding: 5px; 
            background: var(--primary); color: white; border: none; 
            border-radius: 5px; cursor: pointer; font-size: 12px;
        }

        /* RIDE FORM */
        .ride-form {
            background: white;
            margin: 20px;
            padding: 20px;
            border-radius: 15px;
            box-shadow: var(--shadow);
            display: none; /* Hidden by default */
        }
        
        .form-group { margin-bottom: 15px; }
        .form-label { display: block; margin-bottom: 5px; font-size: 14px; color: #666; }
        .form-input { 
            width: 100%; padding: 12px; border: 1px solid #ddd; 
            border-radius: 8px; background: var(--light);
        }
        
        .vehicle-options { display: flex; gap: 10px; margin-bottom: 15px; }
        .vehicle-card {
            flex: 1; border: 2px solid #eee; padding: 10px; 
            border-radius: 10px; text-align: center; cursor: pointer;
        }
        .vehicle-card.active { border-color: var(--primary); background: #e6fffa; }

        /* PAYMENT MODAL */
        .modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.5); display: none;
            justify-content: center; align-items: end;
            z-index: 200;
        }
        
        .modal-content {
            background: white; width: 100%; max-width: 500px;
            border-top-left-radius: 25px; border-top-right-radius: 25px;
            padding: 25px; animation: slideUp 0.3s ease;
        }

        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }

        .payment-methods { display: flex; flex-direction: column; gap: 10px; margin: 20px 0; }
        .pay-method {
            display: flex; justify-content: space-between; align-items: center;
            padding: 15px; border: 1px solid #eee; border-radius: 10px; cursor: pointer;
        }
        .pay-method.selected { border: 2px solid var(--primary); background: #e6fffa; }

        .btn-pay {
            width: 100%; padding: 15px; background: var(--primary);
            color: white; border: none; border-radius: 12px;
            font-size: 16px; font-weight: bold; cursor: pointer;
        }

        /* BOTTOM NAV */
        .bottom-nav {
            position: fixed; bottom: 0; width: 100%; background: white;
            display: flex; justify-content: space-around; padding: 15px 0;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.05);
        }
        .nav-item { text-align: center; color: #aaa; font-size: 12px; cursor: pointer; }
        .nav-item.active { color: var(--primary); }
        .nav-item i { font-size: 20px; margin-bottom: 3px; display: block; }

    </style>
</head>
<body>

    <!-- Header -->
    <header>
        <div class="header-top">
            <div class="logo">Jaluk Tulung</div>
            <div style="background: rgba(255,255,255,0.2); padding: 5px 10px; border-radius: 20px;">
                <i class="fas fa-coins"></i> Rp 150.000
            </div>
        </div>
        <div class="location">
            <i class="fas fa-map-marker-alt"></i> Jl. Ahmad Yani, Tulungagung
        </div>
    </header>

    <!-- Main Menu -->
    <div class="menu-grid">
        <div class="menu-item" onclick="showSection('ride')">
            <div class="menu-icon"><i class="fas fa-motorcycle"></i></div>
            <div class="menu-text">Jaluk Ride</div>
        </div>
        <div class="menu-item" onclick="showSection('car')">
            <div class="menu-icon"><i class="fas fa-car"></i></div>
            <div class="menu-text">Jaluk Car</div>
        </div>
        <div class="menu-item" onclick="showSection('food')">
            <div class="menu-icon"><i class="fas fa-utensils"></i></div>
            <div class="menu-text">Jaluk Food</div>
        </div>
        <div class="menu-item" onclick="alert('Fitur Jasa sedang dalam pengembangan')">
            <div class="menu-icon"><i class="fas fa-hand-holding-heart"></i></div>
            <div class="menu-text">Jasa</div>
        </div>
    </div>

    <!-- Section: Ride (Default) -->
    <div id="ride-section">
        <div class="section-title">Mau kemana hari ini?</div>
        <div class="ride-form" style="display: block;">
            <div class="form-group">
                <label class="form-label">Lokasi Jemput</label>
                <input type="text" class="form-input" value="Posisi Saya Saat Ini" id="pickup">
            </div>
            <div class="form-group">
                <label class="form-label">Tujuan</label>
                <input type="text" class="form-input" placeholder="Cari tujuan..." id="destination">
            </div>
            
            <label class="form-label">Pilih Kendaraan</label>
            <div class="vehicle-options">
                <div class="vehicle-card active" onclick="selectVehicle(this, 'bike')">
                    <i class="fas fa-motorcycle" style="font-size: 20px;"></i>
                    <div style="font-size: 12px; font-weight: bold;">Motor</div>
                    <div style="font-size: 11px; color: #888;">Rp 8.000</div>
                </div>
                <div class="vehicle-card" onclick="selectVehicle(this, 'car')">
                    <i class="fas fa-car" style="font-size: 20px;"></i>
                    <div style="font-size: 12px; font-weight: bold;">Mobil</div>
                    <div style="font-size: 11px; color: #888;">Rp 25.000</div>
                </div>
            </div>

            <button class="btn-pay" onclick="openPayment('Transport', 15000)">Pesan Sekarang</button>
        </div>
    </div>

    <!-- Section: Food -->
    <div id="food-section" style="display: none;">
        <div class="section-title">Lapar? Jaluk Aja!</div>
        <div class="food-container">
            <!-- Item 1 -->
            <div class="food-card">
                <div class="food-img"><i class="fas fa-hamburger fa-2x"></i></div>
                <div class="food-info">
                    <div class="food-name">Burger Tulung</div>
                    <div class="food-price">Rp 25.000</div>
                    <button class="btn-add" onclick="addToCart('Burger Tulung', 25000)">+ Pesan</button>
                </div>
            </div>
            <!-- Item 2 -->
            <div class="food-card">
                <div class="food-img"><i class="fas fa-coffee fa-2x"></i></div>
                <div class="food-info">
                    <div class="food-name">Kopi Gula Aren</div>
                    <div class="food-price">Rp 18.000</div>
                    <button class="btn-add" onclick="addToCart('Kopi Gula Aren', 18000)">+ Pesan</button>
                </div>
            </div>
             <!-- Item 3 -->
             <div class="food-card">
                <div class="food-img"><i class="fas fa-drumstick-bite fa-2x"></i></div>
                <div class="food-info">
                    <div class="food-name">Ayam Geprek</div>
                    <div class="food-price">Rp 15.000</div>
                    <button class="btn-add" onclick="addToCart('Ayam Geprek', 15000)">+ Pesan</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Payment Modal -->
    <div class="modal" id="paymentModal">
        <div class="modal-content">
            <h3 style="margin-bottom: 20px;">Konfirmasi Pembayaran</h3>
            <div style="display: flex; justify-content: space-between; margin-bottom: 20px; font-weight: bold;">
                <span>Total Tagihan</span>
                <span id="totalAmount">Rp 0</span>
            </div>
            
            <div class="payment-methods">
                <div class="pay-method selected" onclick="selectPay(this)">
                    <div><i class="fas fa-wallet" style="color: var(--primary);"></i> Jaluk Pay</div>
                    <i class="fas fa-check-circle" style="color: var(--primary);"></i>
                </div>
                <div class="pay-method" onclick="selectPay(this)">
                    <div><i class="fas fa-qrcode"></i> QRIS</div>
                </div>
                <div class="pay-method" onclick="selectPay(this)">
                    <div><i class="fas fa-money-bill-wave"></i> Tunai</div>
                </div>
            </div>

            <button class="btn-pay" onclick="processPayment()">Bayar Sekarang</button>
            <button style="width: 100%; padding: 10px; background: transparent; border: none; color: #888; margin-top: 10px;" onclick="closeModal()">Batal</button>
        </div>
    </div>

    <!-- Bottom Navigation -->
    <div class="bottom-nav">
        <div class="nav-item active" onclick="showSection('home')">
            <i class="fas fa-home"></i> Home
        </div>
        <div class="nav-item">
            <i class="fas fa-receipt"></i> Pesanan
        </div>
        <div class="nav-item">
            <i class="fas fa-comment-alt"></i> Chat
        </div>
        <div class="nav-item">
            <i class="fas fa-user"></i> Akun
        </div>
    </div>

    <script>
        // Logic Sederhana
        let currentPrice = 0;

        function showSection(section) {
            if(section === 'home') {
                document.getElementById('ride-section').style.display = 'block';
                document.getElementById('food-section').style.display = 'none';
            } else if (section === 'ride' || section === 'car') {
                document.getElementById('ride-section').style.display = 'block';
                document.getElementById('food-section').style.display = 'none';
            } else if (section === 'food') {
                document.getElementById('ride-section').style.display = 'none';
                document.getElementById('food-section').style.display = 'block';
            }
        }

        function selectVehicle(el, type) {
            document.querySelectorAll('.vehicle-card').forEach(card => card.classList.remove('active'));
            el.classList.add('active');
            // Update harga simulasi
            let price = type === 'bike' ? 8000 : 25000;
            // Di aplikasi nyata, ini akan update total
        }

        function addToCart(item, price) {
            alert(item + " ditambahkan ke keranjang!");
            openPayment(item, price);
        }

        function openPayment(item, price) {
            currentPrice = price;
            document.getElementById('totalAmount').innerText = "Rp " + price.toLocaleString('id-ID');
            document.getElementById('paymentModal').style.display = 'flex';
        }

        function closeModal() {
            document.getElementById('paymentModal').style.display = 'none';
        }

        function selectPay(el) {
            document.querySelectorAll('.pay-method').forEach(m => m.classList.remove('selected'));
            el.classList.add('selected');
            // Pindahkan icon check
            let icon = el.querySelector('.fa-check-circle');
            if(!icon) {
                // Hapus icon check dari yang lain (simulasi sederhana)
            }
        }

        function processPayment() {
            const btn = document.querySelector('.btn-pay');
            btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Memproses...';
            
            setTimeout(() => {
                alert("Pembayaran Berhasil! Driver/Pesanan Anda sedang dicari.");
                btn.innerHTML = 'Bayar Sekarang';
                closeModal();
            }, 2000);
        }
    </script>
</body>
</html>
