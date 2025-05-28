    <!DOCTYPE html>
    <html lang="id">
    <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Aplikasi Kasir</title>
    <script src="https://cdn.tailwindcss.com"></script>
    </head>
    <body class="bg-gray-100 p-4 font-sans">
    <div class="max-w-md mx-auto bg-white rounded-xl shadow-md p-4">
        <h1 class="text-xl font-bold mb-4 text-center">Aplikasi Kasir</h1>

        <!-- Produk -->
        <div id="product-list" class="space-y-3">
        <!-- Produk ditambahkan lewat JavaScript -->
        </div>

        <!-- Total dan Tombol -->
        <div class="mt-6">
        <div class="flex justify-between items-center text-lg font-semibold mb-4">
            <span>Total:</span>
            <span id="total-harga" class="text-green-600">Rp 0</span>
        </div>
        <button onclick="bayar()" class="w-full bg-green-600 text-white py-2 rounded-lg mb-2">Bayar</button>
        <button onclick="resetForm()" class="w-full bg-gray-400 text-white py-2 rounded-lg">Reset</button>
        </div>
    </div>

    <script>
        const produk = [
        { id: 1, nama: "Nasi Goreng", harga: 15000 },
        { id: 2, nama: "Mie Ayam", harga: 12000 },
        { id: 3, nama: "Es Teh", harga: 5000 },
        { id: 4, nama: "Kopi", harga: 7000 },
        ];

        const productList = document.getElementById("product-list");
        const totalHargaEl = document.getElementById("total-harga");

        function renderProduk() {
        productList.innerHTML = "";
        produk.forEach((item) => {
            const div = document.createElement("div");
            div.className = "flex justify-between items-center";
            div.innerHTML = `
            <div>
                <p class="font-medium">${item.nama}</p>
                <p class="text-sm text-gray-500">Rp ${item.harga}</p>
            </div>
            <input type="number" min="0" value="0" data-id="${item.id}" class="qty-input w-16 border rounded px-2 py-1 text-right" />
            `;
            productList.appendChild(div);
        });
        }

        function hitungTotal() {
        let total = 0;
        document.querySelectorAll(".qty-input").forEach((input) => {
            const id = parseInt(input.dataset.id);
            const qty = parseInt(input.value);
            const harga = produk.find(p => p.id === id).harga;
            if (!isNaN(qty)) total += qty * harga;
        });
        totalHargaEl.textContent = "Rp " + total.toLocaleString();
        }

        function bayar() {
        hitungTotal();
        alert("Pembayaran berhasil!\n" + totalHargaEl.textContent);
        }

        function resetForm() {
        document.querySelectorAll(".qty-input").forEach(input => input.value = 0);
        totalHargaEl.textContent = "Rp 0";
        }

        document.addEventListener("input", hitungTotal);

        renderProduk();
    </script>
    </body>
    </html>
