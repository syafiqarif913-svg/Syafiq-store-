<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Syafiq Store | Top Up Game Murah Malaysia</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Poppins:wght@400;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        :root { --primary: #f97316; }
        body { 
            font-family: 'Poppins', sans-serif; 
            background-color: #0d1117; 
            color: white;
            transition: background 0.5s ease;
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }
        .ff-bg { background-image: linear-gradient(rgba(13,17,23,0.85), rgba(13,17,23,0.85)), url('https://images7.alphacoders.com/105/1053154.jpg'); }
        .ml-bg { background-image: linear-gradient(rgba(13,17,23,0.85), rgba(13,17,23,0.85)), url('https://wallpaperaccess.com/full/1592357.jpg'); }
        .pubg-bg { background-image: linear-gradient(rgba(13,17,23,0.85), rgba(13,17,23,0.85)), url('https://wallpaperaccess.com/full/1487315.jpg'); }

        .ff-font { font-family: 'Bebas Neue', cursive; letter-spacing: 2px; }
        .glass { background: rgba(22, 27, 34, 0.8); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.1); }
        
        .card-item { 
            cursor: pointer; 
            transition: 0.3s; 
            background: rgba(48, 54, 61, 0.4); 
            border: 2px solid transparent; 
            border-radius: 20px;
        }
        .card-item:hover { transform: scale(1.05); border-color: var(--primary); }
        .active-item { 
            border-color: var(--primary) !important; 
            background: rgba(249, 115, 22, 0.15) !important; 
            box-shadow: 0 0 20px rgba(249, 115, 22, 0.4); 
        }

        .img-diamond {
            width: 60px;
            filter: drop-shadow(0 0 8px rgba(255,255,255,0.5));
            animation: float 3s ease-in-out infinite;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }

        .tab-btn { opacity: 0.6; transition: 0.3s; }
        .tab-active { opacity: 1; transform: scale(1.1); }
    </style>
</head>
<body class="antialiased ff-bg" id="main-body">

    <!-- Header -->
    <header class="p-5 flex justify-between items-center glass sticky top-0 z-50">
        <h1 class="text-3xl ff-font text-orange-500">SYAFIQ <span class="text-white">STORE</span></h1>
        <div class="flex items-center gap-2">
            <span class="w-3 h-3 bg-green-500 rounded-full animate-ping"></span>
            <span class="text-[10px] font-bold uppercase tracking-widest">Sistem Aktif</span>
        </div>
    </header>

    <div class="container mx-auto px-4 py-8 max-w-4xl">
        
        <!-- STEP 1: PILIH GAME -->
        <section class="mb-10 text-center">
            <h2 class="text-xl ff-font mb-6 text-gray-300 italic">--- PILIH GAME ANDA ---</h2>
            <div class="flex justify-around gap-4">
                <button onclick="changeGame('ff')" id="nav-ff" class="tab-btn tab-active">
                    <img src="https://www.freefire.com.my/img/logo.png" class="w-16 h-16 object-contain mb-1">
                    <p class="text-[10px] font-bold">FREE FIRE</p>
                </button>
                <button onclick="changeGame('ml')" id="nav-ml" class="tab-btn">
                    <img src="https://img.icons8.com/color/96/mobile-legends.png" class="w-16 h-16 object-contain mb-1">
                    <p class="text-[10px] font-bold">MLBB</p>
                </button>
                <button onclick="changeGame('pubg')" id="nav-pubg" class="tab-btn">
                    <img src="https://img.icons8.com/color/96/pubg.png" class="w-16 h-16 object-contain mb-1">
                    <p class="text-[10px] font-bold">PUBG</p>
                </button>
            </div>
        </section>

        <!-- STEP 2: INPUT DATA -->
        <section class="glass p-6 rounded-3xl mb-8">
            <h3 class="ff-font text-orange-500 text-lg mb-4 italic"><i class="fa-solid fa-id-card mr-2"></i> MASUKKAN ID PEMAIN</h3>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <input type="number" id="user_id" placeholder="User ID / Player ID" class="w-full bg-black/40 border border-gray-700 p-4 rounded-xl focus:border-orange-500 outline-none font-bold">
                <input type="number" id="zone_id" placeholder="Server ID (Hanya ML)" class="w-full bg-black/40 border border-gray-700 p-4 rounded-xl focus:border-orange-500 outline-none font-bold hidden">
            </div>
        </section>

        <!-- STEP 3: PILIH DIAMOND -->
        <section class="glass p-6 rounded-3xl mb-8">
            <h3 class="ff-font text-orange-500 text-lg mb-6 italic"><i class="fa-solid fa-gem mr-2"></i> PILIH NOMINAL <span id="game-tag"></span></h3>
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-4" id="product-list">
                <!-- Produk diisi oleh JS -->
            </div>
        </section>

        <!-- STEP 4: CHECKOUT -->
        <section class="fixed bottom-0 left-0 w-full p-4 glass md:static md:bg-transparent md:border-none">
            <button onclick="checkout()" class="w-full bg-gradient-to-r from-orange-600 to-red-600 hover:from-orange-500 text-white font-black py-4 rounded-2xl text-xl flex items-center justify-center gap-3 shadow-2xl transition duration-300 active:scale-95">
                BAYAR SEKARANG <i class="fa-brands fa-whatsapp text-2xl"></i>
            </button>
        </section>

    </div>

    <script>
        const products = {
            'ff': {
                tag: 'FREE FIRE',
                items: [
                    { name: '100 Diamonds', price: 'RM 4.20', img: 'https://img.icons8.com/color/96/diamond--v1.png' },
                    { name: '310 Diamonds', price: 'RM 13.00', img: 'https://img.icons8.com/color/96/diamond--v1.png' },
                    { name: '520 Diamonds', price: 'RM 21.50', img: 'https://img.icons8.com/color/96/diamonds.png' },
                    { name: '1060 Diamonds', price: 'RM 42.00', img: 'https://img.icons8.com/color/96/diamonds.png' },
                    { name: 'Weekly Pass', price: 'RM 8.40', img: 'https://img.icons8.com/color/96/membership-card.png' }
                ]
            },
            'ml': {
                tag: 'MOBILE LEGENDS',
                items: [
                    { name: '86 Diamonds', price: 'RM 5.20', img: 'https://img.icons8.com/fluency/96/diamond--v1.png' },
                    { name: '172 Diamonds', price: 'RM 10.40', img: 'https://img.icons8.com/fluency/96/diamond--v1.png' },
                    { name: '257 Diamonds', price: 'RM 15.60', img: 'https://img.icons8.com/fluency/96/diamonds.png' },
                    { name: '706 Diamonds', price: 'RM 42.00', img: 'https://img.icons8.com/fluency/96/diamonds.png' },
                    { name: 'Weekly Pass', price: 'RM 8.90', img: 'https://img.icons8.com/fluency/96/ticket.png' }
                ]
            },
            'pubg': {
                tag: 'PUBG MOBILE',
                items: [
                    { name: '60 UC', price: 'RM 4.00', img: 'https://img.icons8.com/external-flatart-icons-flat-flatarticons/96/external-coin-finance-flatart-icons-flat-flatarticons-1.png' },
                    { name: '325 UC', price: 'RM 19.50', img: 'https://img.icons8.com/external-flatart-icons-flat-flatarticons/96/external-coin-finance-flatart-icons-flat-flatarticons-1.png' },
                    { name: '660 UC', price: 'RM 39.00', img: 'https://img.icons8.com/external-flatart-icons-flat-flatarticons/96/external-coin-finance-flatart-icons-flat-flatarticons-1.png' }
                ]
            }
        };

        let activeGame = 'ff';
        let selectedProduct = "";
        let selectedPrice = "";

        function changeGame(game) {
            activeGame = game;
            selectedProduct = "";
            
            // Tukar BG & Tab
            document.getElementById('main-body').className = `antialiased ${game}-bg`;
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('tab-active'));
            document.getElementById(`nav-${game}`).classList.add('tab-active');
            
            // Show/Hide Zone ID
            document.getElementById('zone_id').classList.toggle('hidden', game !== 'ml');
            document.getElementById('game-tag').innerText = products[game].tag;

            // Render Items
            const container = document.getElementById('product-list');
            container.innerHTML = "";
            products[game].items.forEach(p => {
                const div = document.createElement('div');
                div.className = "card-item p-4 text-center flex flex-col items-center justify-center";
                div.innerHTML = `
                    <img src="${p.img}" class="img-diamond mb-2">
                    <p class="font-bold text-[11px] h-6">${p.name}</p>
                    <p class="text-orange-500 font-black text-xs">${p.price}</p>
                `;
                div.onclick = () => {
                    document.querySelectorAll('.card-item').forEach(c => c.classList.remove('active-item'));
                    div.classList.add('active-item');
                    selectedProduct = p.name;
                    selectedPrice = p.price;
                };
                container.appendChild(div);
            });
        }

        function checkout() {
            const uid = document.getElementById('user_id').value;
            const zid = document.getElementById('zone_id').value;
            const myNum = "601135147359"; // TUKAR NOMBOR ANDA DI SINI

            if (!uid || !selectedProduct) {
                alert("Sila isi ID dan pilih Nominal!");
                return;
            }

            const gameName = products[activeGame].tag;
            const idFull = activeGame === 'ml' ? `${uid}(${zid})` : uid;

            const text = `*ORDER SYAFIQ STORE*%0A` +
                         `----------------------------%0A` +
                         `*Game:* ${gameName}%0A` +
                         `*ID:* ${idFull}%0A` +
                         `*Item:* ${selectedProduct}%0A` +
                         `*Harga:* ${selectedPrice}%0A` +
                         `----------------------------%0A` +
                         `Sila hantar maklumat bayaran.`;

            window.open(`https://wa.me/${myNum}?text=${text}`, '_blank');
        }

        window.onload = () => changeGame('ff');
    </script>
</body>
</html>
