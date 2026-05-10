<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kalkulator HPP & BEP Bisnis</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css">
  <style>
    :root {
      --primary: #0C447C;
      --primary-light: #185FA5;
      --primary-bg: #E6F1FB;
      --success: #3B6D11;
      --success-bg: #EAF3DE;
      --danger: #791F1F;
      --danger-bg: #FCEBEB;
      --danger-border: #E24B4A;
      --bg: #F8FAFC;
      --surface: #FFFFFF;
      --border: rgba(0,0,0,0.12);
      --border-strong: rgba(0,0,0,0.2);
      --text: #1A202C;
      --text-muted: #64748B;
      --text-hint: #94A3B8;
      --radius: 8px;
      --radius-lg: 12px;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Segoe UI', 'Helvetica Neue', Arial, sans-serif;
      background: var(--bg);
      color: var(--text);
      padding: 32px 16px 64px;
      font-size: 14px;
      line-height: 1.6;
    }

    .wrap { max-width: 680px; margin: 0 auto; }

    .header {
      display: flex;
      align-items: flex-start;
      gap: 14px;
      margin-bottom: 28px;
      padding-bottom: 24px;
      border-bottom: 0.5px solid var(--border);
    }
    .logo {
      width: 44px; height: 44px;
      border-radius: var(--radius);
      background: var(--primary);
      display: flex; align-items: center; justify-content: center;
      flex-shrink: 0;
    }
    .logo i { color: var(--primary-bg); font-size: 22px; }
    .header-text h1 { font-size: 20px; font-weight: 600; color: var(--text); margin-bottom: 4px; }
    .header-text p { font-size: 13px; color: var(--text-muted); }

    .steps { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 24px; }
    .step-pill {
      display: flex; align-items: center; gap: 6px;
      background: var(--surface);
      border: 0.5px solid var(--border);
      border-radius: 20px;
      padding: 5px 12px;
      font-size: 12px; color: var(--text-muted);
    }
    .step-pill i { font-size: 14px; color: var(--primary-light); }
    .step-pill b { color: var(--text); font-weight: 500; }

    .card {
      background: var(--surface);
      border: 0.5px solid var(--border);
      border-radius: var(--radius-lg);
      padding: 20px;
      margin-bottom: 14px;
    }
    .card-header { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 16px; }
    .step-badge {
      min-width: 26px; height: 26px; border-radius: 50%;
      background: var(--primary-bg); color: var(--primary);
      font-size: 12px; font-weight: 600;
      display: flex; align-items: center; justify-content: center; flex-shrink: 0;
    }
    .card-title { font-size: 15px; font-weight: 600; color: var(--text); margin-bottom: 2px; }
    .card-desc { font-size: 12px; color: var(--text-muted); line-height: 1.5; }

    label {
      display: block; font-size: 12px; font-weight: 500;
      color: var(--text-muted); margin-bottom: 6px;
      text-transform: uppercase; letter-spacing: 0.04em;
    }

    input[type=number], input[type=text] {
      width: 100%; padding: 10px 12px;
      border: 0.5px solid var(--border-strong);
      border-radius: var(--radius);
      background: var(--surface); color: var(--text);
      font-size: 14px; font-family: inherit;
      transition: border-color 0.2s, box-shadow 0.2s;
    }
    input:focus {
      outline: none; border-color: var(--primary-light);
      box-shadow: 0 0 0 3px rgba(24,95,165,0.12);
    }

    .info-tip {
      font-size: 12px; color: var(--text-muted);
      margin-top: 6px; padding: 7px 10px;
      background: var(--bg); border-radius: var(--radius);
      display: flex; align-items: flex-start; gap: 6px;
    }
    .info-tip i { font-size: 14px; color: var(--text-hint); flex-shrink: 0; margin-top: 1px; }

    .bahan-row { display: flex; gap: 8px; margin-bottom: 8px; align-items: center; }
    .bahan-row input:first-child { flex: 2; }
    .bahan-row input:nth-child(2) { flex: 1; }
    .btn-hapus {
      width: 34px; height: 34px;
      border: 0.5px solid var(--border-strong);
      border-radius: var(--radius);
      background: var(--bg); color: var(--text-muted);
      cursor: pointer; display: flex; align-items: center; justify-content: center;
      flex-shrink: 0; transition: all 0.15s;
    }
    .btn-hapus:hover { background: var(--danger-bg); border-color: var(--danger-border); color: var(--danger); }
    .btn-hapus i { font-size: 15px; }

    .btn-add {
      width: 100%; padding: 9px;
      border: 0.5px dashed var(--primary-light);
      border-radius: var(--radius); background: transparent;
      color: var(--primary-light); cursor: pointer;
      font-size: 13px; font-weight: 500; font-family: inherit;
      display: flex; align-items: center; justify-content: center; gap: 6px;
      margin-top: 8px; transition: background 0.15s;
    }
    .btn-add:hover { background: var(--primary-bg); }
    .btn-add i { font-size: 15px; }

    .hpp-total {
      display: flex; justify-content: space-between; align-items: center;
      margin-top: 12px; padding: 10px 12px;
      background: var(--bg); border-radius: var(--radius); font-size: 13px;
    }
    .hpp-total span { color: var(--text-muted); }
    .hpp-total strong { color: var(--primary); font-weight: 600; }

    .markup-hint {
      display: none; margin-top: 8px; font-size: 12px;
      padding: 8px 11px; border-radius: var(--radius);
      border-left: 2px solid; border-top-left-radius: 0; border-bottom-left-radius: 0;
      line-height: 1.5;
    }
    .markup-hint.ok { background: var(--success-bg); border-left-color: #639922; color: var(--success); }
    .markup-hint.bad { background: var(--danger-bg); border-left-color: var(--danger-border); color: var(--danger); }

    .btn-calc {
      width: 100%; padding: 14px;
      background: var(--primary); color: var(--primary-bg);
      border: none; border-radius: var(--radius);
      font-size: 15px; font-weight: 600; font-family: inherit;
      cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 8px;
      margin-top: 6px; transition: background 0.15s, transform 0.1s;
    }
    .btn-calc:hover { background: var(--primary-light); }
    .btn-calc:active { transform: scale(0.99); }
    .btn-calc i { font-size: 18px; }

    .results { display: none; margin-top: 28px; }
    .divider { border: none; border-top: 0.5px solid var(--border); margin-bottom: 20px; }
    .results-title {
      font-size: 15px; font-weight: 600; color: var(--text);
      margin-bottom: 14px; display: flex; align-items: center; gap: 8px;
    }
    .results-title i { font-size: 18px; color: var(--primary-light); }

    .alert-danger {
      display: none; padding: 12px 14px;
      background: var(--danger-bg);
      border-left: 3px solid var(--danger-border);
      border-radius: var(--radius); border-top-left-radius: 0; border-bottom-left-radius: 0;
      font-size: 13px; color: var(--danger); margin-bottom: 14px; line-height: 1.6;
    }

    .metrics-grid {
      display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 10px; margin-bottom: 14px;
    }
    .metric { background: var(--bg); border-radius: var(--radius); padding: 14px; text-align: center; }
    .metric .mlabel { font-size: 11px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.04em; margin-bottom: 6px; }
    .metric .mvalue { font-size: 20px; font-weight: 600; color: var(--primary); margin-bottom: 3px; }
    .metric .msub { font-size: 11px; color: var(--text-hint); }

    .insight-card {
      background: var(--surface); border: 0.5px solid var(--border);
      border-radius: var(--radius-lg); padding: 20px;
    }
    .insight-card h4 {
      font-size: 14px; font-weight: 600; color: var(--text);
      margin-bottom: 14px; display: flex; align-items: center; gap: 8px;
    }
    .insight-card h4 i { font-size: 16px; color: var(--primary-light); }
    .insight-item {
      display: flex; gap: 10px; margin-bottom: 10px;
      align-items: flex-start; font-size: 13px; color: var(--text-muted); line-height: 1.6;
    }
    .insight-item i { color: var(--primary-light); font-size: 15px; flex-shrink: 0; margin-top: 2px; }
    .insight-item strong { color: var(--text); }

    .rekomendasi {
      margin-top: 12px; padding: 12px 14px;
      background: var(--success-bg); border-radius: var(--radius);
      font-size: 13px; color: var(--success); line-height: 1.6;
    }
    .rekomendasi strong { color: #27500A; }

    @media (max-width: 480px) {
      .steps { display: none; }
      .metrics-grid { grid-template-columns: 1fr 1fr; }
    }
  </style>
</head>
<body>
<div class="wrap">

  <div class="header">
    <div class="logo"><i class="ti ti-chart-bar"></i></div>
    <div class="header-text">
      <h1>Kalkulator HPP & BEP Bisnis</h1>
      <p>Analisis keuangan untuk menghitung <strong>Harga Pokok Produksi (HPP)</strong>, <strong>Break-Even Point (BEP)</strong>, dan rekomendasi strategi harga optimal untuk usaha Anda.</p>
    </div>
  </div>

  <div class="steps">
    <div class="step-pill"><i class="ti ti-circle-1"></i><span><b>Langkah 1</b> — Biaya tetap</span></div>
    <div class="step-pill"><i class="ti ti-circle-2"></i><span><b>Langkah 2</b> — Bahan baku</span></div>
    <div class="step-pill"><i class="ti ti-circle-3"></i><span><b>Langkah 3</b> — Harga jual</span></div>
    <div class="step-pill"><i class="ti ti-circle-4"></i><span><b>Langkah 4</b> — Lihat hasil</span></div>
  </div>

  <div class="card">
    <div class="card-header">
      <div class="step-badge">1</div>
      <div>
        <div class="card-title">Biaya Tetap Operasional</div>
        <div class="card-desc">Biaya yang tetap dikeluarkan setiap bulan, terlepas dari berapa banyak produk yang dibuat — seperti sewa tempat, gaji karyawan tetap, listrik, dan internet.</div>
      </div>
    </div>
    <label for="fixedCost">Total biaya tetap per bulan (Rp)</label>
    <input type="numb
