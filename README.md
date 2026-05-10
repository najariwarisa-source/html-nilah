<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator HPP & BEP Pintar</title>
    <style>
        body { font-family: sans-serif; background-color: #f4f7f6; padding: 20px; color: #333; }
        .container { max-width: 600px; margin: auto; background: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
        h2 { text-align: center; color: #2c3e50; }
        .section { margin-bottom: 20px; border-bottom: 1px solid #eee; padding-bottom: 15px; }
        label { display: block; margin-bottom: 5px; font-weight: bold; font-size: 0.9em; }
        input { width: 100%; padding: 10px; margin-bottom: 10px; border: 1px solid #ddd; border-radius: 6px; box-sizing: border-box; }
        button { width: 100%; padding: 12px; background-color: #27ae60; color: white; border: none; border-radius: 6px; cursor: pointer; font-size: 1em; font-weight: bold; }
        button:hover { background-color: #219150; }
        .result { margin-top: 20px; padding: 15px; background-color: #e8f8f5; border-radius: 6px; display: none; }
        .result h3 { margin-top: 0; color: #16a085; }
        .insight { font-size: 0.9em; color: #666; font-style: italic; margin-top: 10px; }
    </style>
</head>
<body>

<div class="container">
    <h2>Kalkulator Bisnis Pintar</h2>
    
    <div class="section">
        <h3>1. Biaya Tetap (Fixed Cost)</h3>
        <label>Total Biaya Bulanan (Sewa, Gaji, Listrik)</label>
        <input type="number" id="fixedCost" placeholder="Contoh: 5000000">
    </div>

    <div class="section">
        <h3>2. Biaya Variabel (HPP per Unit)</h3>
        <label>Bahan Baku & Kemasan per Produk</label>
        <input type="number" id="variableCost" placeholder="Contoh: 8000">
    </div>

    <div class="section">
        <h3>3. Strategi Harga</h3>
        <label>Harga Jual per Unit</label>
        <input type="number" id="sellingPrice" placeholder="Contoh: 15000">
    </div>

    <button onclick="hitungBEP()">Hitung Kelayakan Bisnis</button>

    <div id="resultArea" class="result">
        <h3>Hasil Analisis:</h3>
        <p id="hppResult"></p>
        <p id="bepResult"></p>
        <div id="insightArea" class="insight"></div>
    </div>
</div>

<script>
    function hitungBEP() {
        const fc = parseFloat(document.getElementById('fixedCost').value);
        const vc = parseFloat(document.getElementById('variableCost').value);
        const price = parseFloat(document.getElementById('sellingPrice').value);
        
        if (isNaN(fc) || isNaN(vc) || isNaN(price)) {
            alert("Harap isi semua kolom dengan angka.");
            return;
        }

        const marginPerUnit = price - vc;
        const bepUnit = Math.ceil(fc / marginPerUnit);
        const hppPercent = (vc / price * 100).toFixed(1);

        const resultArea = document.getElementById('resultArea');
        const hppText = document.getElementById('hppResult');
        const bepText = document.getElementById('bepResult');
        const insightText = document.getElementById('insightArea');

        if (marginPerUnit <= 0) {
            hppText.innerHTML = "❌ <strong>Peringatan:</strong> Harga jual lebih rendah atau sama dengan biaya produksi!";
            bepText.innerHTML = "";
            insightText.innerHTML = "Kamu akan rugi di setiap penjualan. Naikkan harga atau tekan biaya bahan baku.";
        } else {
            hppText.innerHTML = `💰 <strong>Margin per Unit:</strong> Rp ${marginPerUnit.toLocaleString('id-ID')}`;
            bepText.innerHTML = `🎯 <strong>Titik Impas (BEP):</strong> ${bepUnit.toLocaleString('id-ID')} unit per bulan.`;
            insightText.innerHTML = `Insight: Biaya produksi menghabiskan ${hppPercent}% dari harga jualmu. Penjualan ke-${(bepUnit + 1)} adalah keuntungan murnimu!`;
        }

        resultArea.style.display = 'block';
    }
</script>

</body>
</html>
