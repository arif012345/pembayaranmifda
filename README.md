<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Pembayaran Siswa - MTs Miftahul Huda</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <style>
        :root {
            --primary: #3498db;
            --primary-dark: #2980b9;
            --secondary: #2ecc71;
            --secondary-dark: #27ae60;
            --danger: #e74c3c;
            --danger-dark: #c0392b;
            --warning: #f39c12;
            --warning-dark: #d35400;
            --dark: #2c3e50;
            --dark-light: #34495e;
            --light: #ecf0f1;
            --gray: #95a5a6;
            --gray-light: #bdc3c7;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
        }
        
        .container {
            display: flex;
            min-height: 100vh;
        }
        
        /* Sidebar Styles */
        .sidebar {
            width: 250px;
            background-color: var(--dark);
            color: white;
            transition: all 0.3s;
        }
        
        .sidebar-header {
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.2);
            text-align: center;
        }
        
        .sidebar-menu {
            padding: 0;
            list-style: none;
        }
        
        .sidebar-menu li {
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }
        
        .sidebar-menu a {
            display: block;
            padding: 15px 20px;
            color: white;
            text-decoration: none;
            transition: all 0.3s;
        }
        
        .sidebar-menu a:hover, .sidebar-menu a.active {
            background-color: var(--primary);
            padding-left: 25px;
        }
        
        .sidebar-menu i {
            margin-right: 10px;
        }
        
        /* Main Content Styles */
        .main-content {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
        }
        
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }
        
        .page-title {
            font-size: 24px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .card-header {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #eee;
        }
        
        /* Form Styles */
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
        }
        
        button {
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
        }
        
        .btn-primary {
            background-color: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: var(--primary-dark);
        }
        
        .btn-success {
            background-color: var(--secondary);
            color: white;
        }
        
        .btn-success:hover {
            background-color: var(--secondary-dark);
        }
        
        .btn-danger {
            background-color: var(--danger);
            color: white;
        }
        
        .btn-danger:hover {
            background-color: var(--danger-dark);
        }
        
        .btn-warning {
            background-color: var(--warning);
            color: white;
        }
        
        .btn-warning:hover {
            background-color: var(--warning-dark);
        }
        
        /* Table Styles */
        table {
            width: 100%;
            border-collapse: collapse;
        }
        
        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        
        th {
            background-color: #f8f9fa;
            font-weight: 600;
        }
        
        tr:hover {
            background-color: #f5f5f5;
        }
        
        .badge {
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
        }
        
        .badge-success {
            background-color: #d4edda;
            color: #155724;
        }
        
        .badge-danger {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        .badge-warning {
            background-color: #fff3cd;
            color: #856404;
        }
        
        .badge-info {
            background-color: #d1ecf1;
            color: #0c5460;
        }
        
        /* Dashboard Stats */
        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .stat-card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 28px;
            font-weight: 700;
            margin: 10px 0;
        }
        
        .stat-label {
            color: #6c757d;
            font-size: 14px;
        }
        
        /* Tab Styles */
        .tabs {
            display: flex;
            border-bottom: 1px solid #ddd;
            margin-bottom: 20px;
        }
        
        .tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 2px solid transparent;
        }
        
        .tab.active {
            border-bottom: 2px solid var(--primary);
            color: var(--primary);
            font-weight: 600;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        /* Alert Styles */
        .alert {
            padding: 15px;
            border-radius: 4px;
            margin-bottom: 20px;
        }
        
        .alert-success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        
        .alert-danger {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        
        .alert-warning {
            background-color: #fff3cd;
            color: #856404;
            border: 1px solid #ffeaa7;
        }
        
        /* Page Content Styles */
        .page-content {
            display: none;
        }
        
        .page-content.active {
            display: block;
        }
        
        /* Autocomplete Styles */
        .autocomplete-items {
            position: absolute;
            border: 1px solid #d4d4d4;
            border-bottom: none;
            border-top: none;
            z-index: 99;
            top: 100%;
            left: 0;
            right: 0;
            background: white;
        }
        
        .autocomplete-items div {
            padding: 10px;
            cursor: pointer;
            background-color: #fff;
            border-bottom: 1px solid #d4d4d4;
        }
        
        .autocomplete-items div:hover {
            background-color: #e9e9e9;
        }
        
        .autocomplete-active {
            background-color: var(--primary) !important;
            color: white;
        }
        
        .autocomplete-container {
            position: relative;
        }
        
        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
        }
        
        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 20px;
            border-radius: 8px;
            width: 80%;
            max-width: 600px;
            max-height: 80vh;
            overflow-y: auto;
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }
        
        .close:hover {
            color: black;
        }
        
        /* Kuitansi Styles */
        .kuitansi {
            border: 2px solid #000;
            padding: 20px;
            background: white;
            max-width: 500px;
            margin: 0 auto;
        }
        
        .kuitansi-header {
            text-align: center;
            border-bottom: 2px solid #000;
            padding-bottom: 10px;
            margin-bottom: 15px;
        }
        
        .kuitansi-detail {
            margin-bottom: 15px;
        }
        
        .kuitansi-footer {
            text-align: center;
            margin-top: 30px;
        }
        
        /* Utility Classes */
        .text-right {
            text-align: right;
        }
        
        .text-center {
            text-align: center;
        }
        
        .d-none {
            display: none;
        }
        
        .mt-3 {
            margin-top: 15px;
        }
        
        .mb-3 {
            margin-bottom: 15px;
        }
        
        .p-3 {
            padding: 15px;
        }
        
        .cursor-pointer {
            cursor: pointer;
        }
        
        /* Excel Import/Export Styles */
        .excel-section {
            border: 2px dashed #ddd;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .excel-section:hover {
            border-color: var(--primary);
        }
        
        .excel-template {
            display: inline-block;
            margin: 10px;
            padding: 10px 15px;
            background-color: var(--secondary);
            color: white;
            border-radius: 4px;
            text-decoration: none;
            transition: all 0.3s;
        }
        
        .excel-template:hover {
            background-color: var(--secondary-dark);
        }
        
        .excel-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            justify-content: center;
        }
        
        /* Footer Styles */
        .app-footer {
            text-align: center;
            margin-top: 30px;
            padding: 15px;
            color: #6c757d;
            font-size: 12px;
            border-top: 1px solid #eee;
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: auto;
            }
            
            .stats-container {
                grid-template-columns: 1fr;
            }
            
            .modal-content {
                width: 95%;
                margin: 10% auto;
            }
            
            .excel-actions {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Sidebar -->
        <div class="sidebar">
            <div class="sidebar-header">
                <h2>MTs Miftahul Huda</h2>
                <p>Aplikasi Pembayaran</p>
            </div>
            <ul class="sidebar-menu">
                <li><a href="#" class="active" data-page="dashboard"><i>📊</i> Dashboard</a></li>
                <li><a href="#" data-page="siswa"><i>👨‍🎓</i> Data Siswa</a></li>
                <li><a href="#" data-page="tagihan"><i>💰</i> Input Tagihan</a></li>
                <li><a href="#" data-page="pembayaran"><i>💳</i> Input Pembayaran</a></li>
                <li><a href="#" data-page="laporan"><i>📋</i> Laporan</a></li>
                <li><a href="#" data-page="setting"><i>⚙️</i> Setting</a></li>
            </ul>
        </div>
        
        <!-- Main Content -->
        <div class="main-content">
            <!-- Header -->
            <div class="header">
                <h1 class="page-title">Dashboard</h1>
                <div id="current-date"></div>
            </div>
            
            <!-- Dashboard Content -->
            <div id="dashboard-content" class="page-content active">
                <div class="stats-container">
                    <div class="stat-card">
                        <div class="stat-label">Total Siswa</div>
                        <div class="stat-value" id="total-siswa">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Pembayaran Hari Ini</div>
                        <div class="stat-value" id="pembayaran-hari-ini">Rp 0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Siswa Belum Lunas</div>
                        <div class="stat-value" id="siswa-belum-lunas">0</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Total Tunggakan</div>
                        <div class="stat-value" id="total-tunggakan">Rp 0</div>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">Pembayaran Terbaru</div>
                    <table id="recent-payments">
                        <thead>
                            <tr>
                                <th>Nama Siswa</th>
                                <th>Kelas</th>
                                <th>Jenis Tagihan</th>
                                <th>Jumlah</th>
                                <th>Tanggal</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Data akan diisi oleh JavaScript -->
                        </tbody>
                    </table>
                </div>

                <!-- Tambahan: Footer dengan credit -->
                <div class="app-footer">
                    <p>powered by AishCell 085655379028</p>
                </div>
            </div>
            
            <!-- Data Siswa Content -->
            <div id="siswa-content" class="page-content">
                <div class="card">
                    <div class="card-header">Input Data Siswa</div>
                    <form id="form-siswa">
                        <div class="form-group">
                            <label for="nis">NIS</label>
                            <input type="text" id="nis" required>
                        </div>
                        <div class="form-group">
                            <label for="nama-siswa">Nama Siswa</label>
                            <input type="text" id="nama-siswa" required>
                        </div>
                        <div class="form-group">
                            <label for="kelas-siswa">Kelas</label>
                            <select id="kelas-siswa" required>
                                <option value="">Pilih Kelas</option>
                                <option value="7">Kelas 7</option>
                                <option value="8a">Kelas 8A</option>
                                <option value="8b">Kelas 8B</option>
                                <option value="9">Kelas 9</option>
                            </select>
                        </div>
                        <button type="submit" class="btn-primary">Simpan Data Siswa</button>
                    </form>
                </div>
                
                <div class="card">
                    <div class="card-header">Import Data Siswa dari Excel</div>
                    <div class="excel-section">
                        <p>Download template Excel untuk import data siswa:</p>
                        <a href="#" id="download-template" class="excel-template">📥 Download Template Excel</a>
                        
                        <div class="form-group mt-3">
                            <label for="file-import">Upload File Excel</label>
                            <input type="file" id="file-import" accept=".xlsx, .xls">
                        </div>
                        
                        <div class="excel-actions">
                            <button id="btn-import" class="btn-success">Import Data</button>
                            <button id="btn-preview" class="btn-primary">Preview Data</button>
                        </div>
                    </div>
                    
                    <div id="preview-container" class="mt-3" style="display: none;">
                        <h4>Preview Data yang Akan Diimport</h4>
                        <div id="preview-table-container" style="max-height: 300px; overflow-y: auto;">
                            <table id="preview-table">
                                <thead>
                                    <tr>
                                        <th>NIS</th>
                                        <th>Nama</th>
                                        <th>Kelas</th>
                                        <th>Status</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <!-- Data preview akan diisi oleh JavaScript -->
                                </tbody>
                            </table>
                        </div>
                        <div class="mt-3">
                            <button id="btn-confirm-import" class="btn-success">Konfirmasi Import</button>
                            <button id="btn-cancel-import" class="btn-danger">Batal</button>
                        </div>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">Daftar Siswa</div>
                    <table id="table-siswa">
                        <thead>
                            <tr>
                                <th>NIS</th>
                                <th>Nama</th>
                                <th>Kelas</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Data akan diisi oleh JavaScript -->
                        </tbody>
                    </table>
                </div>

                <!-- Tambahan: Footer dengan credit -->
                <div class="app-footer">
                    <p>powered by AishCell 085655379028</p>
                </div>
            </div>
            
            <!-- Input Tagihan Content -->
            <div id="tagihan-content" class="page-content">
                <div class="card">
                    <div class="card-header">Input Tagihan</div>
                    <form id="form-tagihan">
                        <div class="form-group">
                            <label for="jenis-tagihan">Jenis Tagihan</label>
                            <input type="text" id="jenis-tagihan" required>
                        </div>
                        <div class="form-group">
                            <label for="kategori-tagihan">Kategori Tagihan</label>
                            <select id="kategori-tagihan" required>
                                <option value="">Pilih Kategori</option>
                                <option value="bulanan">Bulanan</option>
                                <option value="semesteran">Semesteran</option>
                                <option value="tahunan">Tahunan</option>
                                <option value="sekali-bayar">Sekali Bayar</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="jumlah-tagihan">Jumlah Tagihan</label>
                            <input type="number" id="jumlah-tagihan" required>
                        </div>
                        <div class="form-group">
                            <label for="kelas-tagihan">Kelas yang Dikenakan</label>
                            <select id="kelas-tagihan" required>
                                <option value="">Pilih Kelas</option>
                                <option value="semua">Semua Kelas</option>
                                <option value="7">Kelas 7</option>
                                <option value="8a">Kelas 8A</option>
                                <option value="8b">Kelas 8B</option>
                                <option value="9">Kelas 9</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="keterangan-tagihan">Keterangan</label>
                            <textarea id="keterangan-tagihan" rows="3"></textarea>
                        </div>
                        <button type="submit" class="btn-primary">Simpan Tagihan</button>
                    </form>
                </div>
                
                <div class="card">
                    <div class="card-header">Daftar Tagihan</div>
                    <table id="table-tagihan">
                        <thead>
                            <tr>
                                <th>Jenis Tagihan</th>
                                <th>Kategori</th>
                                <th>Jumlah</th>
                                <th>Kelas</th>
                                <th>Keterangan</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Data akan diisi oleh JavaScript -->
                        </tbody>
                    </table>
                </div>

                <!-- Tambahan: Footer dengan credit -->
                <div class="app-footer">
                    <p>powered by AishCell 085655379028</p>
                </div>
            </div>
            
            <!-- Input Pembayaran Content -->
            <div id="pembayaran-content" class="page-content">
                <div class="card">
                    <div class="card-header">Input Pembayaran</div>
                    <form id="form-pembayaran">
                        <div class="form-group">
                            <label for="cari-siswa">Cari Siswa (Nama atau NIS)</label>
                            <div class="autocomplete-container">
                                <input type="text" id="cari-siswa" placeholder="Ketik nama atau NIS siswa..." required>
                            </div>
                            <input type="hidden" id="nis-pembayaran">
                            <div id="info-kelas-siswa" class="mt-3" style="display: none;">
                                <p><strong>Kelas Siswa:</strong> <span id="kelas-siswa-terpilih"></span></p>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="jenis-pembayaran">Jenis Tagihan</label>
                            <select id="jenis-pembayaran" required>
                                <option value="">Pilih Jenis Tagihan</option>
                            </select>
                            <div id="info-tagihan" class="mt-3" style="display: none;">
                                <p><strong>Total Tagihan:</strong> <span id="total-tagihan"></span></p>
                                <p><strong>Sudah Dibayar:</strong> <span id="sudah-dibayar"></span></p>
                                <p><strong>Sisa Tagihan:</strong> <span id="sisa-tagihan"></span></p>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="jumlah-pembayaran">Jumlah Pembayaran</label>
                            <input type="number" id="jumlah-pembayaran" required>
                        </div>
                        <div class="form-group">
                            <label for="tanggal-pembayaran">Tanggal Pembayaran</label>
                            <input type="date" id="tanggal-pembayaran" required>
                        </div>
                        <div class="form-group">
                            <label for="keterangan-pembayaran">Keterangan</label>
                            <textarea id="keterangan-pembayaran" rows="3"></textarea>
                        </div>
                        <button type="submit" class="btn-primary">Simpan Pembayaran</button>
                    </form>
                </div>
                
                <div class="card">
                    <div class="card-header">Riwayat Pembayaran</div>
                    <table id="table-pembayaran">
                        <thead>
                            <tr>
                                <th>NIS</th>
                                <th>Nama</th>
                                <th>Jenis Tagihan</th>
                                <th>Jumlah</th>
                                <th>Tanggal</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody>
                            <!-- Data akan diisi oleh JavaScript -->
                        </tbody>
                    </table>
                </div>

                <!-- Tambahan: Footer dengan credit -->
                <div class="app-footer">
                    <p>powered by AishCell 085655379028</p>
                </div>
            </div>
            
            <!-- Laporan Content -->
            <div id="laporan-content" class="page-content">
                <div class="tabs">
                    <div class="tab active" data-tab="laporan-siswa">Laporan Per Siswa</div>
                    <div class="tab" data-tab="laporan-kelas">Laporan Per Kelas</div>
                    <div class="tab" data-tab="laporan-tagihan">Laporan Per Tagihan</div>
                </div>
                
                <div id="laporan-siswa" class="tab-content active">
                    <div class="card">
                        <div class="card-header">Laporan Pembayaran Per Siswa</div>
                        <div class="form-group">
                            <label for="filter-kelas">Filter Kelas</label>
                            <select id="filter-kelas">
                                <option value="semua">Semua Kelas</option>
                                <option value="7">Kelas 7</option>
                                <option value="8a">Kelas 8A</option>
                                <option value="8b">Kelas 8B</option>
                                <option value="9">Kelas 9</option>
                            </select>
                        </div>
                        <div class="excel-actions mb-3">
                            <button id="btn-export-siswa" class="btn-success">📊 Export ke Excel</button>
                        </div>
                        <table id="table-laporan-siswa">
                            <thead>
                                <tr>
                                    <th>NIS</th>
                                    <th>Nama</th>
                                    <th>Kelas</th>
                                    <th>Total Tagihan</th>
                                    <th>Total Dibayar</th>
                                    <th>Sisa</th>
                                    <th>Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Data akan diisi oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>

                    <!-- Tambahan: Footer dengan credit -->
                    <div class="app-footer">
                        <p>powered by AishCell 085655379028</p>
                    </div>
                </div>
                
                <div id="laporan-kelas" class="tab-content">
                    <div class="card">
                        <div class="card-header">Laporan Pembayaran Per Kelas</div>
                        <div class="excel-actions mb-3">
                            <button id="btn-export-kelas" class="btn-success">📊 Export ke Excel</button>
                        </div>
                        <table id="table-laporan-kelas">
                            <thead>
                                <tr>
                                    <th>Kelas</th>
                                    <th>Jumlah Siswa</th>
                                    <th>Total Tagihan</th>
                                    <th>Total Dibayar</th>
                                    <th>Sisa</th>
                                    <th>Persentase</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Data akan diisi oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>

                    <!-- Tambahan: Footer dengan credit -->
                    <div class="app-footer">
                        <p>powered by AishCell 085655379028</p>
                    </div>
                </div>
                
                <div id="laporan-tagihan" class="tab-content">
                    <div class="card">
                        <div class="card-header">Laporan Pembayaran Per Tagihan</div>
                        <div class="excel-actions mb-3">
                            <button id="btn-export-tagihan" class="btn-success">📊 Export ke Excel</button>
                        </div>
                        <table id="table-laporan-tagihan">
                            <thead>
                                <tr>
                                    <th>Jenis Tagihan</th>
                                    <th>Kategori</th>
                                    <th>Kelas</th>
                                    <th>Total Tagihan</th>
                                    <th>Total Dibayar</th>
                                    <th>Sisa</th>
                                    <th>Persentase</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Data akan diisi oleh JavaScript -->
                            </tbody>
                        </table>
                    </div>

                    <!-- Tambahan: Footer dengan credit -->
                    <div class="app-footer">
                        <p>powered by AishCell 085655379028</p>
                    </div>
                </div>
            </div>
            
            <!-- Setting Content -->
            <div id="setting-content" class="page-content">
                <div class="card">
                    <div class="card-header">Backup dan Restore Data</div>
                    <div class="form-group">
                        <button id="btn-backup" class="btn-primary">Backup Data</button>
                        <p class="mt-3">Backup data akan mengunduh file JSON berisi semua data aplikasi.</p>
                    </div>
                    <div class="form-group">
                        <label for="file-restore">Restore Data</label>
                        <input type="file" id="file-restore" accept=".json">
                        <button id="btn-restore" class="btn-warning mt-3">Restore Data</button>
                        <p class="mt-3">Peringatan: Restore data akan menggantikan semua data yang ada saat ini.</p>
                    </div>
                </div>
                
                <div class="card">
                    <div class="card-header">Reset Data</div>
                    <p>Hati-hati! Tindakan ini akan menghapus semua data dan tidak dapat dibatalkan.</p>
                    <button id="btn-reset" class="btn-danger mt-3">Reset Semua Data</button>
                </div>

                <!-- Tambahan: Footer dengan credit -->
                <div class="app-footer">
                    <p>powered by AishCell 085655379028</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Rincian Siswa -->
    <div id="modal-rincian" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <div class="card">
                <div class="card-header">Rincian Pembayaran Siswa</div>
                <div id="rincian-siswa-content">
                    <!-- Konten rincian akan diisi oleh JavaScript -->
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Kuitansi -->
    <div id="modal-kuitansi" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <div id="kuitansi-content">
                <!-- Konten kuitansi akan diisi oleh JavaScript -->
            </div>
            <div class="text-center mt-3">
                <button id="btn-cetak-kuitansi" class="btn-primary">Cetak Kuitansi</button>
            </div>
        </div>
    </div>

    <script>
        // Inisialisasi data jika belum ada
        function initializeData() {
            if (!localStorage.getItem('siswa')) {
                localStorage.setItem('siswa', JSON.stringify([]));
            }
            if (!localStorage.getItem('tagihan')) {
                localStorage.setItem('tagihan', JSON.stringify([]));
            }
            if (!localStorage.getItem('pembayaran')) {
                localStorage.setItem('pembayaran', JSON.stringify([]));
            }
        }

        // Format angka ke Rupiah
        function formatRupiah(angka) {
            return new Intl.NumberFormat('id-ID', {
                style: 'currency',
                currency: 'IDR'
            }).format(angka);
        }

        // Format tanggal
        function formatTanggal(tanggal) {
            return new Date(tanggal).toLocaleDateString('id-ID');
        }

        // Ambil data dari localStorage
        function getData(key) {
            return JSON.parse(localStorage.getItem(key)) || [];
        }

        // Simpan data ke localStorage
        function saveData(key, data) {
            localStorage.setItem(key, JSON.stringify(data));
        }

        // ==================== NAVIGASI MENU ====================
        document.querySelectorAll('.sidebar-menu a').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                
                // Hapus kelas active dari semua menu
                document.querySelectorAll('.sidebar-menu a').forEach(item => {
                    item.classList.remove('active');
                });
                
                // Tambah kelas active ke menu yang diklik
                this.classList.add('active');
                
                // Sembunyikan semua konten
                document.querySelectorAll('.page-content').forEach(content => {
                    content.classList.remove('active');
                });
                
                // Tampilkan konten yang sesuai
                const pageId = this.getAttribute('data-page');
                const contentElement = document.getElementById(pageId + '-content');
                if (contentElement) {
                    contentElement.classList.add('active');
                }
                
                // Update judul halaman
                const pageTitles = {
                    'dashboard': 'Dashboard',
                    'siswa': 'Data Siswa',
                    'tagihan': 'Input Tagihan',
                    'pembayaran': 'Input Pembayaran',
                    'laporan': 'Laporan',
                    'setting': 'Setting'
                };
                document.querySelector('.page-title').textContent = pageTitles[pageId] || 'Aplikasi Pembayaran';
                
                // Refresh data jika diperlukan
                if (pageId === 'dashboard') {
                    updateDashboard();
                } else if (pageId === 'laporan') {
                    updateLaporan();
                } else if (pageId === 'siswa') {
                    updateTableSiswa();
                } else if (pageId === 'tagihan') {
                    updateTableTagihan();
                } else if (pageId === 'pembayaran') {
                    updateTablePembayaran();
                    // Reset form pembayaran
                    document.getElementById('form-pembayaran').reset();
                    document.getElementById('info-kelas-siswa').style.display = 'none';
                    document.getElementById('info-tagihan').style.display = 'none';
                    initializeAutocomplete();
                }
            });
        });

        // Navigasi tab laporan
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', function() {
                // Hapus kelas active dari semua tab
                document.querySelectorAll('.tab').forEach(item => {
                    item.classList.remove('active');
                });
                
                // Tambah kelas active ke tab yang diklik
                this.classList.add('active');
                
                // Sembunyikan semua konten tab
                document.querySelectorAll('.tab-content').forEach(content => {
                    content.classList.remove('active');
                });
                
                // Tampilkan konten tab yang sesuai
                const tabId = this.getAttribute('data-tab');
                document.getElementById(tabId).classList.add('active');
            });
        });

        // ==================== FUNGSI AUTOKOMPLIT ====================
        function autocomplete(inp, arr) {
            let currentFocus;
            
            inp.addEventListener("input", function(e) {
                let a, b, i, val = this.value;
                closeAllLists();
                if (!val) { return false; }
                currentFocus = -1;
                
                a = document.createElement("DIV");
                a.setAttribute("id", this.id + "autocomplete-list");
                a.setAttribute("class", "autocomplete-items");
                this.parentNode.appendChild(a);
                
                for (i = 0; i < arr.length; i++) {
                    if (arr[i].text.substr(0, val.length).toUpperCase() == val.toUpperCase() || 
                        arr[i].nis.substr(0, val.length) == val) {
                        b = document.createElement("DIV");
                        b.innerHTML = "<strong>" + arr[i].text.substr(0, val.length) + "</strong>";
                        b.innerHTML += arr[i].text.substr(val.length);
                        b.innerHTML += " <small>(NIS: " + arr[i].nis + " - Kelas: " + arr[i].kelas + ")</small>";
                        b.innerHTML += "<input type='hidden' value='" + arr[i].text + "'>";
                        b.innerHTML += "<input type='hidden' data-nis='" + arr[i].nis + "' data-kelas='" + arr[i].kelas + "'>";
                        b.addEventListener("click", function(e) {
                            inp.value = this.getElementsByTagName("input")[0].value;
                            document.getElementById("nis-pembayaran").value = this.getElementsByTagName("input")[1].getAttribute("data-nis");
                            
                            // Tampilkan info kelas siswa
                            const kelasSiswa = this.getElementsByTagName("input")[1].getAttribute("data-kelas");
                            document.getElementById("kelas-siswa-terpilih").textContent = kelasSiswa;
                            document.getElementById("info-kelas-siswa").style.display = "block";
                            
                            // Update opsi tagihan berdasarkan kelas siswa
                            updateJenisTagihanOptions(kelasSiswa);
                            
                            closeAllLists();
                        });
                        a.appendChild(b);
                    }
                }
            });
            
            inp.addEventListener("keydown", function(e) {
                let x = document.getElementById(this.id + "autocomplete-list");
                if (x) x = x.getElementsByTagName("div");
                if (e.keyCode == 40) {
                    currentFocus++;
                    addActive(x);
                } else if (e.keyCode == 38) {
                    currentFocus--;
                    addActive(x);
                } else if (e.keyCode == 13) {
                    e.preventDefault();
                    if (currentFocus > -1) {
                        if (x) x[currentFocus].click();
                    }
                }
            });
            
            function addActive(x) {
                if (!x) return false;
                removeActive(x);
                if (currentFocus >= x.length) currentFocus = 0;
                if (currentFocus < 0) currentFocus = (x.length - 1);
                x[currentFocus].classList.add("autocomplete-active");
            }
            
            function removeActive(x) {
                for (let i = 0; i < x.length; i++) {
                    x[i].classList.remove("autocomplete-active");
                }
            }
            
            function closeAllLists(elmnt) {
                let x = document.getElementsByClassName("autocomplete-items");
                for (let i = 0; i < x.length; i++) {
                    if (elmnt != x[i] && elmnt != inp) {
                        x[i].parentNode.removeChild(x[i]);
                    }
                }
            }
            
            document.addEventListener("click", function (e) {
                closeAllLists(e.target);
            });
        }

        // Update opsi jenis tagihan di form pembayaran berdasarkan kelas siswa
        function updateJenisTagihanOptions(kelasSiswa) {
            const select = document.getElementById('jenis-pembayaran');
            const tagihan = getData('tagihan');
            
            // Kosongkan opsi
            select.innerHTML = '<option value="">Pilih Jenis Tagihan</option>';
            
            // Tambah opsi untuk setiap tagihan yang sesuai dengan kelas siswa
            tagihan.forEach(t => {
                if (t.kelas === 'semua' || t.kelas === kelasSiswa) {
                    const option = document.createElement('option');
                    option.value = t.jenis;
                    option.textContent = `${t.jenis} (${t.kategori}) - ${formatRupiah(t.jumlah)}`;
                    option.setAttribute('data-tagihan-id', t.id);
                    select.appendChild(option);
                }
            });
            
            // Reset info tagihan
            document.getElementById('info-tagihan').style.display = 'none';
            
            // Tambah event listener untuk menampilkan info tagihan saat dipilih
            select.addEventListener('change', function() {
                const jenisTagihan = this.value;
                const nis = document.getElementById('nis-pembayaran').value;
                
                if (jenisTagihan && nis) {
                    updateInfoTagihan(nis, jenisTagihan);
                }
            });
        }

        // Update info tagihan (total, sudah dibayar, sisa)
        function updateInfoTagihan(nis, jenisTagihan) {
            const tagihan = getData('tagihan').find(t => t.jenis === jenisTagihan);
            const pembayaran = getData('pembayaran');
            
            if (!tagihan) return;
            
            // Hitung total yang sudah dibayar
            const totalDibayar = pembayaran
                .filter(p => p.nis === nis && p.jenis === jenisTagihan)
                .reduce((total, p) => total + p.jumlah, 0);
            
            const sisaTagihan = tagihan.jumlah - totalDibayar;
            
            // Update tampilan
            document.getElementById('total-tagihan').textContent = formatRupiah(tagihan.jumlah);
            document.getElementById('sudah-dibayar').textContent = formatRupiah(totalDibayar);
            document.getElementById('sisa-tagihan').textContent = formatRupiah(sisaTagihan);
            
            // Tampilkan info tagihan
            document.getElementById('info-tagihan').style.display = 'block';
            
            // Set jumlah pembayaran maksimal ke sisa tagihan
            document.getElementById('jumlah-pembayaran').max = sisaTagihan;
        }

        // Inisialisasi autocomplete
        function initializeAutocomplete() {
            const siswa = getData('siswa');
            const arrSiswa = siswa.map(s => ({
                text: `${s.nama} (${s.kelas})`,
                nis: s.nis,
                kelas: s.kelas
            }));
            
            autocomplete(document.getElementById("cari-siswa"), arrSiswa);
        }

        // ==================== FORM HANDLING ====================
        // Form Data Siswa
        document.getElementById('form-siswa').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const nis = document.getElementById('nis').value;
            const nama = document.getElementById('nama-siswa').value;
            const kelas = document.getElementById('kelas-siswa').value;
            
            // Cek apakah NIS sudah ada
            const siswa = getData('siswa');
            const nisExists = siswa.some(s => s.nis === nis);
            
            if (nisExists) {
                alert('NIS sudah terdaftar!');
                return;
            }
            
            // Tambah siswa baru
            siswa.push({ nis, nama, kelas });
            saveData('siswa', siswa);
            
            // Reset form
            this.reset();
            
            // Update tabel siswa
            updateTableSiswa();
            
            alert('Data siswa berhasil disimpan!');
        });

        // Form Tagihan
        document.getElementById('form-tagihan').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const jenis = document.getElementById('jenis-tagihan').value;
            const kategori = document.getElementById('kategori-tagihan').value;
            const jumlah = parseInt(document.getElementById('jumlah-tagihan').value);
            const kelas = document.getElementById('kelas-tagihan').value;
            const keterangan = document.getElementById('keterangan-tagihan').value;
            
            // Tambah tagihan baru
            const tagihan = getData('tagihan');
            tagihan.push({
                id: Date.now().toString(),
                jenis,
                kategori,
                jumlah,
                kelas,
                keterangan,
                tanggal: new Date().toISOString()
            });
            
            saveData('tagihan', tagihan);
            
            // Reset form
            this.reset();
            
            // Update tabel tagihan
            updateTableTagihan();
            
            alert('Tagihan berhasil disimpan!');
        });

        // Form Pembayaran
        document.getElementById('form-pembayaran').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const nis = document.getElementById('nis-pembayaran').value;
            const jenis = document.getElementById('jenis-pembayaran').value;
            const jumlah = parseInt(document.getElementById('jumlah-pembayaran').value);
            const tanggal = document.getElementById('tanggal-pembayaran').value;
            const keterangan = document.getElementById('keterangan-pembayaran').value;
            
            // Cek apakah siswa dipilih
            if (!nis) {
                alert('Silakan pilih siswa terlebih dahulu!');
                return;
            }
            
            // Cek apakah siswa ada
            const siswa = getData('siswa');
            const siswaData = siswa.find(s => s.nis === nis);
            
            if (!siswaData) {
                alert('Siswa dengan NIS tersebut tidak ditemukan!');
                return;
            }
            
            // Cek apakah tagihan ada
            const tagihan = getData('tagihan');
            const tagihanData = tagihan.find(t => t.jenis === jenis);
            
            if (!tagihanData) {
                alert('Jenis tagihan tidak valid!');
                return;
            }
            
            // Cek apakah tagihan sesuai dengan kelas siswa
            if (tagihanData.kelas !== 'semua' && tagihanData.kelas !== siswaData.kelas) {
                alert(`Tagihan ini hanya untuk kelas ${tagihanData.kelas.toUpperCase()}, sedangkan siswa ini berada di kelas ${siswaData.kelas.toUpperCase()}!`);
                return;
            }
            
            // Cek apakah siswa sudah lunas untuk tagihan ini
            const pembayaran = getData('pembayaran');
            const totalDibayar = pembayaran
                .filter(p => p.nis === nis && p.jenis === jenis)
                .reduce((total, p) => total + p.jumlah, 0);
            
            if (totalDibayar >= tagihanData.jumlah) {
                alert('Siswa sudah melunasi tagihan ini! Pembayaran ditolak.');
                return;
            }
            
            // Cek apakah pembayaran melebihi sisa tagihan
            const sisaTagihan = tagihanData.jumlah - totalDibayar;
            if (jumlah > sisaTagihan) {
                alert(`Pembayaran melebihi sisa tagihan! Sisa tagihan: ${formatRupiah(sisaTagihan)}`);
                return;
            }
            
            // Simpan pembayaran
            const pembayaranId = Date.now().toString();
            pembayaran.push({
                id: pembayaranId,
                nis,
                jenis,
                jumlah,
                tanggal,
                keterangan
            });
            
            saveData('pembayaran', pembayaran);
            
            // Reset form
            document.getElementById('cari-siswa').value = '';
            document.getElementById('nis-pembayaran').value = '';
            document.getElementById('form-pembayaran').reset();
            document.getElementById('info-kelas-siswa').style.display = 'none';
            document.getElementById('info-tagihan').style.display = 'none';
            
            // Update tabel pembayaran
            updateTablePembayaran();
            
            // Tampilkan kuitansi
            tampilkanKuitansi(pembayaranId, nis, siswaData.nama, siswaData.kelas, jenis, jumlah, tanggal, keterangan);
            
            alert('Pembayaran berhasil disimpan!');
        });

        // ==================== FUNGSI TABEL ====================
        // Update tabel siswa
        function updateTableSiswa() {
            const tbody = document.querySelector('#table-siswa tbody');
            const siswa = getData('siswa');
            
            tbody.innerHTML = '';
            
            siswa.forEach(s => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${s.nis}</td>
                    <td>${s.nama}</td>
                    <td>${s.kelas}</td>
                    <td>
                        <button class="btn-danger btn-hapus-siswa" data-nis="${s.nis}">Hapus</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
            
            // Tambah event listener untuk tombol hapus
            document.querySelectorAll('.btn-hapus-siswa').forEach(btn => {
                btn.addEventListener('click', function() {
                    const nis = this.getAttribute('data-nis');
                    
                    if (confirm(`Apakah Anda yakin ingin menghapus siswa dengan NIS ${nis}?`)) {
                        // Hapus siswa
                        let siswa = getData('siswa');
                        siswa = siswa.filter(s => s.nis !== nis);
                        saveData('siswa', siswa);
                        
                        // Hapus pembayaran terkait
                        let pembayaran = getData('pembayaran');
                        pembayaran = pembayaran.filter(p => p.nis !== nis);
                        saveData('pembayaran', pembayaran);
                        
                        // Update tabel
                        updateTableSiswa();
                        updateTablePembayaran();
                        
                        alert('Siswa berhasil dihapus!');
                    }
                });
            });
        }

        // Update tabel tagihan
        function updateTableTagihan() {
            const tbody = document.querySelector('#table-tagihan tbody');
            const tagihan = getData('tagihan');
            
            tbody.innerHTML = '';
            
            tagihan.forEach(t => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${t.jenis}</td>
                    <td><span class="badge badge-info">${t.kategori}</span></td>
                    <td>${formatRupiah(t.jumlah)}</td>
                    <td>${t.kelas === 'semua' ? 'Semua Kelas' : 'Kelas ' + t.kelas.toUpperCase()}</td>
                    <td>${t.keterangan || '-'}</td>
                    <td>
                        <button class="btn-danger btn-hapus-tagihan" data-id="${t.id}">Hapus</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
            
            // Tambah event listener untuk tombol hapus
            document.querySelectorAll('.btn-hapus-tagihan').forEach(btn => {
                btn.addEventListener('click', function() {
                    const id = this.getAttribute('data-id');
                    
                    if (confirm('Apakah Anda yakin ingin menghapus tagihan ini?')) {
                        // Hapus tagihan
                        let tagihan = getData('tagihan');
                        tagihan = tagihan.filter(t => t.id !== id);
                        saveData('tagihan', tagihan);
                        
                        // Hapus pembayaran terkait
                        let pembayaran = getData('pembayaran');
                        pembayaran = pembayaran.filter(p => p.jenis !== tagihan.find(t => t.id === id)?.jenis);
                        saveData('pembayaran', pembayaran);
                        
                        // Update tabel
                        updateTableTagihan();
                        updateTablePembayaran();
                        
                        alert('Tagihan berhasil dihapus!');
                    }
                });
            });
        }

        // Update tabel pembayaran
        function updateTablePembayaran() {
            const tbody = document.querySelector('#table-pembayaran tbody');
            const pembayaran = getData('pembayaran');
            const siswa = getData('siswa');
            
            tbody.innerHTML = '';
            
            pembayaran.forEach(p => {
                const siswaData = siswa.find(s => s.nis === p.nis);
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${p.nis}</td>
                    <td>${siswaData ? siswaData.nama : 'Tidak Diketahui'}</td>
                    <td>${p.jenis}</td>
                    <td>${formatRupiah(p.jumlah)}</td>
                    <td>${formatTanggal(p.tanggal)}</td>
                    <td>
                        <button class="btn-primary btn-kuitansi" data-id="${p.id}">Kuitansi</button>
                        <button class="btn-danger btn-hapus-pembayaran" data-id="${p.id}">Hapus</button>
                    </td>
                `;
                tbody.appendChild(row);
            });
            
            // Tambah event listener untuk tombol kuitansi
            document.querySelectorAll('.btn-kuitansi').forEach(btn => {
                btn.addEventListener('click', function() {
                    const id = this.getAttribute('data-id');
                    const pembayaranData = getData('pembayaran').find(p => p.id === id);
                    const siswaData = getData('siswa').find(s => s.nis === pembayaranData.nis);
                    
                    if (pembayaranData && siswaData) {
                        tampilkanKuitansi(
                            pembayaranData.id,
                            pembayaranData.nis,
                            siswaData.nama,
                            siswaData.kelas,
                            pembayaranData.jenis,
                            pembayaranData.jumlah,
                            pembayaranData.tanggal,
                            pembayaranData.keterangan
                        );
                    }
                });
            });
            
            // Tambah event listener untuk tombol hapus
            document.querySelectorAll('.btn-hapus-pembayaran').forEach(btn => {
                btn.addEventListener('click', function() {
                    const id = this.getAttribute('data-id');
                    
                    if (confirm('Apakah Anda yakin ingin menghapus pembayaran ini?')) {
                        // Hapus pembayaran
                        let pembayaran = getData('pembayaran');
                        pembayaran = pembayaran.filter(p => p.id !== id);
                        saveData('pembayaran', pembayaran);
                        
                        // Update tabel
                        updateTablePembayaran();
                        
                        alert('Pembayaran berhasil dihapus!');
                    }
                });
            });
        }

        // ==================== DASHBOARD ====================
        // Update dashboard
        function updateDashboard() {
            const siswa = getData('siswa');
            const tagihan = getData('tagihan');
            const pembayaran = getData('pembayaran');
            
            // Total siswa
            document.getElementById('total-siswa').textContent = siswa.length;
            
            // Pembayaran hari ini
            const today = new Date().toISOString().split('T')[0];
            const pembayaranHariIni = pembayaran
                .filter(p => p.tanggal === today)
                .reduce((total, p) => total + p.jumlah, 0);
            document.getElementById('pembayaran-hari-ini').textContent = formatRupiah(pembayaranHariIni);
            
            // Hitung siswa yang belum lunas dan total tunggakan
            let siswaBelumLunas = 0;
            let totalTunggakan = 0;
            
            siswa.forEach(s => {
                const tagihanSiswa = tagihan.filter(t => t.kelas === 'semua' || t.kelas === s.kelas);
                let totalTagihanSiswa = 0;
                let totalDibayarSiswa = 0;
                
                tagihanSiswa.forEach(t => {
                    totalTagihanSiswa += t.jumlah;
                    
                    const pembayaranSiswa = pembayaran
                        .filter(p => p.nis === s.nis && p.jenis === t.jenis)
                        .reduce((total, p) => total + p.jumlah, 0);
                    
                    totalDibayarSiswa += pembayaranSiswa;
                });
                
                if (totalDibayarSiswa < totalTagihanSiswa) {
                    siswaBelumLunas++;
                    totalTunggakan += (totalTagihanSiswa - totalDibayarSiswa);
                }
            });
            
            document.getElementById('siswa-belum-lunas').textContent = siswaBelumLunas;
            document.getElementById('total-tunggakan').textContent = formatRupiah(totalTunggakan);
            
            // Pembayaran terbaru
            const tbody = document.querySelector('#recent-payments tbody');
            tbody.innerHTML = '';
            
            const pembayaranTerbaru = pembayaran
                .sort((a, b) => new Date(b.tanggal) - new Date(a.tanggal))
                .slice(0, 5);
            
            pembayaranTerbaru.forEach(p => {
                const siswaData = siswa.find(s => s.nis === p.nis);
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${siswaData ? siswaData.nama : 'Tidak Diketahui'}</td>
                    <td>${siswaData ? siswaData.kelas : '-'}</td>
                    <td>${p.jenis}</td>
                    <td>${formatRupiah(p.jumlah)}</td>
                    <td>${formatTanggal(p.tanggal)}</td>
                `;
                tbody.appendChild(row);
            });
        }

        // ==================== LAPORAN ====================
        // Update laporan
        function updateLaporan() {
            updateLaporanSiswa();
            updateLaporanKelas();
            updateLaporanTagihan();
        }

        // Update laporan per siswa
        function updateLaporanSiswa() {
            const tbody = document.querySelector('#table-laporan-siswa tbody');
            const siswa = getData('siswa');
            const tagihan = getData('tagihan');
            const pembayaran = getData('pembayaran');
            const filterKelas = document.getElementById('filter-kelas').value;
            
            tbody.innerHTML = '';
            
            siswa.forEach(s => {
                if (filterKelas !== 'semua' && s.kelas !== filterKelas) return;
                
                const tagihanSiswa = tagihan.filter(t => t.kelas === 'semua' || t.kelas === s.kelas);
                let totalTagihanSiswa = 0;
                let totalDibayarSiswa = 0;
                
                tagihanSiswa.forEach(t => {
                    totalTagihanSiswa += t.jumlah;
                    
                    const pembayaranSiswa = pembayaran
                        .filter(p => p.nis === s.nis && p.jenis === t.jenis)
                        .reduce((total, p) => total + p.jumlah, 0);
                    
                    totalDibayarSiswa += pembayaranSiswa;
                });
                
                const sisa = totalTagihanSiswa - totalDibayarSiswa;
                const status = sisa <= 0 ? 
                    '<span class="badge badge-success">LUNAS</span>' : 
                    '<span class="badge badge-danger">BELUM LUNAS</span>';
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${s.nis}</td>
                    <td class="cursor-pointer" onclick="tampilkanRincianSiswa('${s.nis}')">${s.nama}</td>
                    <td>${s.kelas}</td>
                    <td>${formatRupiah(totalTagihanSiswa)}</td>
                    <td>${formatRupiah(totalDibayarSiswa)}</td>
                    <td>${formatRupiah(sisa)}</td>
                    <td>${status}</td>
                `;
                tbody.appendChild(row);
            });
            
            // Event listener untuk filter kelas
            document.getElementById('filter-kelas').addEventListener('change', updateLaporanSiswa);
        }

        // Tampilkan rincian siswa
        function tampilkanRincianSiswa(nis) {
            const siswa = getData('siswa').find(s => s.nis === nis);
            const tagihan = getData('tagihan').filter(t => t.kelas === 'semua' || t.kelas === siswa.kelas);
            const pembayaran = getData('pembayaran').filter(p => p.nis === nis);
            
            let content = `
                <h3>Rincian Pembayaran: ${siswa.nama} (${siswa.kelas})</h3>
                <table class="mt-3">
                    <thead>
                        <tr>
                            <th>Jenis Tagihan</th>
                            <th>Kategori</th>
                            <th>Total Tagihan</th>
                            <th>Total Dibayar</th>
                            <th>Sisa</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            
            tagihan.forEach(t => {
                const totalDibayar = pembayaran
                    .filter(p => p.jenis === t.jenis)
                    .reduce((total, p) => total + p.jumlah, 0);
                
                const sisa = t.jumlah - totalDibayar;
                const status = sisa <= 0 ? 
                    '<span class="badge badge-success">LUNAS</span>' : 
                    '<span class="badge badge-danger">BELUM LUNAS</span>';
                
                content += `
                    <tr>
                        <td>${t.jenis}</td>
                        <td><span class="badge badge-info">${t.kategori}</span></td>
                        <td>${formatRupiah(t.jumlah)}</td>
                        <td>${formatRupiah(totalDibayar)}</td>
                        <td>${formatRupiah(sisa)}</td>
                        <td>${status}</td>
                    </tr>
                `;
            });
            
            content += `
                    </tbody>
                </table>
                <div class="mt-3">
                    <h4>Riwayat Pembayaran:</h4>
                    <table class="mt-3">
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>Jenis Tagihan</th>
                                <th>Jumlah</th>
                                <th>Keterangan</th>
                            </tr>
                        </thead>
                        <tbody>
            `;
            
            pembayaran.forEach(p => {
                content += `
                    <tr>
                        <td>${formatTanggal(p.tanggal)}</td>
                        <td>${p.jenis}</td>
                        <td>${formatRupiah(p.jumlah)}</td>
                        <td>${p.keterangan || '-'}</td>
                    </tr>
                `;
            });
            
            content += `
                        </tbody>
                    </table>
                </div>
            `;
            
            document.getElementById('rincian-siswa-content').innerHTML = content;
            modalRincian.style.display = 'block';
        }

        // Update laporan per kelas
        function updateLaporanKelas() {
            const tbody = document.querySelector('#table-laporan-kelas tbody');
            const siswa = getData('siswa');
            const tagihan = getData('tagihan');
            const pembayaran = getData('pembayaran');
            
            tbody.innerHTML = '';
            
            const kelasList = ['7', '8a', '8b', '9'];
            
            kelasList.forEach(kelas => {
                const siswaKelas = siswa.filter(s => s.kelas === kelas);
                let totalTagihanKelas = 0;
                let totalDibayarKelas = 0;
                
                siswaKelas.forEach(s => {
                    const tagihanSiswa = tagihan.filter(t => t.kelas === 'semua' || t.kelas === s.kelas);
                    
                    tagihanSiswa.forEach(t => {
                        totalTagihanKelas += t.jumlah;
                        
                        const pembayaranSiswa = pembayaran
                            .filter(p => p.nis === s.nis && p.jenis === t.jenis)
                            .reduce((total, p) => total + p.jumlah, 0);
                        
                        totalDibayarKelas += pembayaranSiswa;
                    });
                });
                
                const sisa = totalTagihanKelas - totalDibayarKelas;
                const persentase = totalTagihanKelas > 0 ? 
                    Math.round((totalDibayarKelas / totalTagihanKelas) * 100) : 0;
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>Kelas ${kelas.toUpperCase()}</td>
                    <td>${siswaKelas.length}</td>
                    <td>${formatRupiah(totalTagihanKelas)}</td>
                    <td>${formatRupiah(totalDibayarKelas)}</td>
                    <td>${formatRupiah(sisa)}</td>
                    <td>${persentase}%</td>
                `;
                tbody.appendChild(row);
            });
        }

        // Update laporan per tagihan
        function updateLaporanTagihan() {
            const tbody = document.querySelector('#table-laporan-tagihan tbody');
            const siswa = getData('siswa');
            const tagihan = getData('tagihan');
            const pembayaran = getData('pembayaran');
            
            tbody.innerHTML = '';
            
            tagihan.forEach(t => {
                const siswaTerkena = siswa.filter(s => t.kelas === 'semua' || t.kelas === s.kelas);
                const totalTagihan = t.jumlah * siswaTerkena.length;
                let totalDibayar = 0;
                
                siswaTerkena.forEach(s => {
                    const pembayaranSiswa = pembayaran
                        .filter(p => p.nis === s.nis && p.jenis === t.jenis)
                        .reduce((total, p) => total + p.jumlah, 0);
                    
                    totalDibayar += pembayaranSiswa;
                });
                
                const sisa = totalTagihan - totalDibayar;
                const persentase = totalTagihan > 0 ? 
                    Math.round((totalDibayar / totalTagihan) * 100) : 0;
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${t.jenis}</td>
                    <td><span class="badge badge-info">${t.kategori}</span></td>
                    <td>${t.kelas === 'semua' ? 'Semua Kelas' : 'Kelas ' + t.kelas.toUpperCase()}</td>
                    <td>${formatRupiah(totalTagihan)}</td>
                    <td>${formatRupiah(totalDibayar)}</td>
                    <td>${formatRupiah(sisa)}</td>
                    <td>${persentase}%</td>
                `;
                tbody.appendChild(row);
            });
        }

        // ==================== MODAL FUNCTIONALITY ====================
        const modalRincian = document.getElementById('modal-rincian');
        const modalKuitansi = document.getElementById('modal-kuitansi');
        const closeButtons = document.querySelectorAll('.close');

        closeButtons.forEach(btn => {
            btn.addEventListener('click', function() {
                modalRincian.style.display = 'none';
                modalKuitansi.style.display = 'none';
            });
        });

        window.addEventListener('click', function(e) {
            if (e.target == modalRincian) {
                modalRincian.style.display = 'none';
            }
            if (e.target == modalKuitansi) {
                modalKuitansi.style.display = 'none';
            }
        });

        // Tampilkan kuitansi
        function tampilkanKuitansi(pembayaranId, nis, nama, kelas, jenis, jumlah, tanggal, keterangan) {
            const kuitansiContent = document.getElementById('kuitansi-content');
            kuitansiContent.innerHTML = `
                <div class="kuitansi">
                    <div class="kuitansi-header">
                        <h3>MTs MIFTAHUL HUDA</h3>
                        <p>KUITANSI PEMBAYARAN</p>
                    </div>
                    <div class="kuitansi-detail">
                        <p><strong>No. Kuitansi:</strong> ${pembayaranId}</p>
                        <p><strong>Tanggal:</strong> ${formatTanggal(tanggal)}</p>
                        <p><strong>NIS:</strong> ${nis}</p>
                        <p><strong>Nama Siswa:</strong> ${nama}</p>
                        <p><strong>Kelas:</strong> ${kelas}</p>
                        <p><strong>Jenis Tagihan:</strong> ${jenis}</p>
                        <p><strong>Jumlah Pembayaran:</strong> ${formatRupiah(jumlah)}</p>
                        ${keterangan ? `<p><strong>Keterangan:</strong> ${keterangan}</p>` : ''}
                    </div>
                    <div class="kuitansi-footer">
                        <p>Terima kasih atas pembayarannya</p>
                        <br><br>
                        <p>_________________________</p>
                        <p>Bendahara</p>
                    </div>
                </div>
            `;
            
            modalKuitansi.style.display = 'block';
        }

        // Cetak kuitansi
        document.getElementById('btn-cetak-kuitansi').addEventListener('click', function() {
            const kuitansiContent = document.getElementById('kuitansi-content').innerHTML;
            const originalContent = document.body.innerHTML;
            
            document.body.innerHTML = kuitansiContent;
            window.print();
            document.body.innerHTML = originalContent;
            location.reload();
        });

        // ==================== EXCEL IMPORT/EXPORT ====================
        // Fungsi untuk download template Excel
        function downloadTemplateExcel() {
            // Data untuk template
            const templateData = [
                ['NIS', 'Nama', 'Kelas'],
                ['001', 'Ahmad Surya', '7'],
                ['002', 'Budi Santoso', '8a'],
                ['003', 'Citra Lestari', '8b'],
                ['004', 'Dewi Anggraini', '9'],
                ['', '', ''],
                ['CATATAN:'],
                ['- Kolom harus diisi sesuai format'],
                ['- Kelas yang valid: 7, 8a, 8b, 9'],
                ['- Pastikan NIS unik untuk setiap siswa']
            ];
            
            // Buat workbook
            const wb = XLSX.utils.book_new();
            const ws = XLSX.utils.aoa_to_sheet(templateData);
            
            // Atur lebar kolom
            const colWidths = [
                { wch: 10 }, // NIS
                { wch: 25 }, // Nama
                { wch: 10 }  // Kelas
            ];
            ws['!cols'] = colWidths;
            
            // Tambah worksheet ke workbook
            XLSX.utils.book_append_sheet(wb, ws, 'Template Siswa');
            
            // Download file
            XLSX.writeFile(wb, 'template_import_siswa.xlsx');
        }

        // Fungsi untuk membaca file Excel
        function readExcelFile(file, callback) {
            const reader = new FileReader();
            
            reader.onload = function(e) {
                const data = new Uint8Array(e.target.result);
                const workbook = XLSX.read(data, { type: 'array' });
                
                // Ambil sheet pertama
                const firstSheet = workbook.Sheets[workbook.SheetNames[0]];
                const jsonData = XLSX.utils.sheet_to_json(firstSheet, { header: 1 });
                
                callback(jsonData);
            };
            
            reader.readAsArrayBuffer(file);
        }

        // Fungsi untuk validasi data siswa dari Excel
        function validateStudentData(data) {
            const errors = [];
            const validKelas = ['7', '8a', '8b', '9'];
            const existingStudents = getData('siswa');
            const existingNIS = existingStudents.map(s => s.nis);
            
            // Lewati header (baris pertama)
            for (let i = 1; i < data.length; i++) {
                const row = data[i];
                
                // Skip baris kosong
                if (!row || row.length < 3 || !row[0]) continue;
                
                const nis = String(row[0]).trim();
                const nama = String(row[1]).trim();
                const kelas = String(row[2]).trim().toLowerCase();
                
                // Validasi NIS
                if (!nis) {
                    errors.push(`Baris ${i+1}: NIS tidak boleh kosong`);
                } else if (existingNIS.includes(nis)) {
                    errors.push(`Baris ${i+1}: NIS ${nis} sudah terdaftar`);
                }
                
                // Validasi Nama
                if (!nama) {
                    errors.push(`Baris ${i+1}: Nama tidak boleh kosong`);
                }
                
                // Validasi Kelas
                if (!kelas) {
                    errors.push(`Baris ${i+1}: Kelas tidak boleh kosong`);
                } else if (!validKelas.includes(kelas)) {
                    errors.push(`Baris ${i+1}: Kelas '${kelas}' tidak valid. Harus salah satu dari: 7, 8a, 8b, 9`);
                }
            }
            
            return errors;
        }

        // Fungsi untuk preview data dari Excel
        function previewExcelData(data) {
            const previewTable = document.getElementById('preview-table');
            const tbody = previewTable.querySelector('tbody');
            tbody.innerHTML = '';
            
            const existingStudents = getData('siswa');
            const existingNIS = existingStudents.map(s => s.nis);
            
            let validCount = 0;
            let duplicateCount = 0;
            
            // Lewati header (baris pertama)
            for (let i = 1; i < data.length; i++) {
                const row = data[i];
                
                // Skip baris kosong
                if (!row || row.length < 3 || !row[0]) continue;
                
                const nis = String(row[0]).trim();
                const nama = String(row[1]).trim();
                const kelas = String(row[2]).trim().toLowerCase();
                
                const isValid = nis && nama && kelas && ['7', '8a', '8b', '9'].includes(kelas);
                const isDuplicate = existingNIS.includes(nis);
                
                const tr = document.createElement('tr');
                
                if (!isValid) {
                    tr.style.backgroundColor = '#f8d7da';
                } else if (isDuplicate) {
                    tr.style.backgroundColor = '#fff3cd';
                    duplicateCount++;
                } else {
                    validCount++;
                }
                
                tr.innerHTML = `
                    <td>${nis}</td>
                    <td>${nama}</td>
                    <td>${kelas}</td>
                    <td>
                        ${!isValid ? '<span class="badge badge-danger">Data tidak valid</span>' : 
                          isDuplicate ? '<span class="badge badge-warning">NIS sudah ada</span>' : 
                          '<span class="badge badge-success">Valid</span>'}
                    </td>
                `;
                
                tbody.appendChild(tr);
            }
            
            // Tampilkan summary
            const summary = document.createElement('div');
            summary.className = 'alert alert-info mt-3';
            summary.innerHTML = `
                <strong>Summary:</strong><br>
                - Data valid: ${validCount}<br>
                - Data duplikat: ${duplicateCount}<br>
                - Total data: ${data.length - 1}
            `;
            
            document.getElementById('preview-container').appendChild(summary);
        }

        // Fungsi untuk import data siswa dari Excel
        function importStudentData(data) {
            const students = getData('siswa');
            const existingNIS = students.map(s => s.nis);
            let importedCount = 0;
            let skippedCount = 0;
            
            // Lewati header (baris pertama)
            for (let i = 1; i < data.length; i++) {
                const row = data[i];
                
                // Skip baris kosong
                if (!row || row.length < 3 || !row[0]) continue;
                
                const nis = String(row[0]).trim();
                const nama = String(row[1]).trim();
                const kelas = String(row[2]).trim().toLowerCase();
                
                // Validasi data
                if (!nis || !nama || !kelas || !['7', '8a', '8b', '9'].includes(kelas)) {
                    skippedCount++;
                    continue;
                }
                
                // Cek duplikasi
                if (existingNIS.includes(nis)) {
                    skippedCount++;
                    continue;
                }
                
                // Tambah siswa baru
                students.push({ nis, nama, kelas });
                existingNIS.push(nis);
                importedCount++;
            }
            
            // Simpan data
            saveData('siswa', students);
            
            return { imported: importedCount, skipped: skippedCount };
        }

        // Fungsi untuk export laporan ke Excel
        function exportLaporanToExcel(data, filename, sheetName) {
            const wb = XLSX.utils.book_new();
            const ws = XLSX.utils.json_to_sheet(data);
            
            // Tambah worksheet ke workbook
            XLSX.utils.book_append_sheet(wb, ws, sheetName);
            
            // Download file
            XLSX.writeFile(wb, filename);
        }

        // Fungsi untuk mendapatkan data laporan siswa untuk export
        function getLaporanSiswaForExport() {
            const siswa = getData('siswa');
            const tagihan = getData('tagihan');
            const pembayaran = getData('pembayaran');
            const filterKelas = document.getElementById('filter-kelas').value;
            
            const data = [];
            
            siswa.forEach(s => {
                if (filterKelas !== 'semua' && s.kelas !== filterKelas) return;
                
                const tagihanSiswa = tagihan.filter(t => t.kelas === 'semua' || t.kelas === s.kelas);
                let totalTagihanSiswa = 0;
                let totalDibayarSiswa = 0;
                
                // Detail per jenis tagihan
                const detailTagihan = [];
                
                tagihanSiswa.forEach(t => {
                    const pembayaranSiswa = pembayaran
                        .filter(p => p.nis === s.nis && p.jenis === t.jenis)
                        .reduce((total, p) => total + p.jumlah, 0);
                    
                    totalTagihanSiswa += t.jumlah;
                    totalDibayarSiswa += pembayaranSiswa;
                    
                    detailTagihan.push({
                        jenis: t.jenis,
                        total: t.jumlah,
                        dibayar: pembayaranSiswa,
                        sisa: t.jumlah - pembayaranSiswa,
                        status: pembayaranSiswa >= t.jumlah ? 'LUNAS' : 'BELUM LUNAS'
                    });
                });
                
                const sisa = totalTagihanSiswa - totalDibayarSiswa;
                const status = sisa <= 0 ? 'LUNAS' : 'BELUM LUNAS';
                
                // Data utama
                data.push({
                    'NIS': s.nis,
                    'Nama': s.nama,
                    'Kelas': s.kelas,
                    'Total Tagihan': totalTagihanSiswa,
                    'Total Dibayar': totalDibayarSiswa,
                    'Sisa': sisa,
                    'Status': status
                });
                
                // Tambah detail untuk setiap jenis tagihan
                detailTagihan.forEach(d => {
                    data.push({
                        'NIS': '',
                        'Nama': `  - ${d.jenis}`,
                        'Kelas': '',
                        'Total Tagihan': d.total,
                        'Total Dibayar': d.dibayar,
                        'Sisa': d.sisa,
                        'Status': d.status
                    });
                });
                
                // Tambah baris kosong sebagai pemisah
                data.push({
                    'NIS': '',
                    'Nama': '',
                    'Kelas': '',
                    'Total Tagihan': '',
                    'Total Dibayar': '',
                    'Sisa': '',
                    'Status': ''
                });
            });
            
            return data;
        }

        // Fungsi untuk mendapatkan data laporan kelas untuk export
        function getLaporanKelasForExport() {
            const siswa = getData('siswa');
            const tagihan = getData('tagihan');
            const pembayaran = getData('pembayaran');
            
            const data = [];
            const kelasList = ['7', '8a', '8b', '9'];
            
            kelasList.forEach(kelas => {
                const siswaKelas = siswa.filter(s => s.kelas === kelas);
                let totalTagihanKelas = 0;
                let totalDibayarKelas = 0;
                
                siswaKelas.forEach(s => {
                    const tagihanSiswa = tagihan.filter(t => t.kelas === 'semua' || t.kelas === s.kelas);
                    
                    tagihanSiswa.forEach(t => {
                        totalTagihanKelas += t.jumlah;
                        
                        const pembayaranSiswa = pembayaran
                            .filter(p => p.nis === s.nis && p.jenis === t.jenis)
                            .reduce((total, p) => total + p.jumlah, 0);
                        
                        totalDibayarKelas += pembayaranSiswa;
                    });
                });
                
                const sisa = totalTagihanKelas - totalDibayarKelas;
                const persentase = totalTagihanKelas > 0 ? 
                    Math.round((totalDibayarKelas / totalTagihanKelas) * 100) : 0;
                
                data.push({
                    'Kelas': `Kelas ${kelas.toUpperCase()}`,
                    'Jumlah Siswa': siswaKelas.length,
                    'Total Tagihan': totalTagihanKelas,
                    'Total Dibayar': totalDibayarKelas,
                    'Sisa': sisa,
                    'Persentase': `${persentase}%`
                });
            });
            
            return data;
        }

        // Fungsi untuk mendapatkan data laporan tagihan untuk export
        function getLaporanTagihanForExport() {
            const siswa = getData('siswa');
            const tagihan = getData('tagihan');
            const pembayaran = getData('pembayaran');
            
            const data = [];
            
            tagihan.forEach(t => {
                const siswaTerkena = siswa.filter(s => t.kelas === 'semua' || t.kelas === s.kelas);
                const totalTagihan = t.jumlah * siswaTerkena.length;
                let totalDibayar = 0;
                
                siswaTerkena.forEach(s => {
                    const pembayaranSiswa = pembayaran
                        .filter(p => p.nis === s.nis && p.jenis === t.jenis)
                        .reduce((total, p) => total + p.jumlah, 0);
                    
                    totalDibayar += pembayaranSiswa;
                });
                
                const sisa = totalTagihan - totalDibayar;
                const persentase = totalTagihan > 0 ? 
                    Math.round((totalDibayar / totalTagihan) * 100) : 0;
                
                data.push({
                    'Jenis Tagihan': t.jenis,
                    'Kategori': t.kategori,
                    'Kelas': t.kelas === 'semua' ? 'Semua Kelas' : `Kelas ${t.kelas.toUpperCase()}`,
                    'Total Tagihan': totalTagihan,
                    'Total Dibayar': totalDibayar,
                    'Sisa': sisa,
                    'Persentase': `${persentase}%`
                });
            });
            
            return data;
        }

        // Event listener untuk download template
        document.getElementById('download-template').addEventListener('click', function(e) {
            e.preventDefault();
            downloadTemplateExcel();
        });

        // Event listener untuk preview data
        document.getElementById('btn-preview').addEventListener('click', function() {
            const fileInput = document.getElementById('file-import');
            const file = fileInput.files[0];
            
            if (!file) {
                alert('Pilih file Excel terlebih dahulu!');
                return;
            }
            
            readExcelFile(file, function(data) {
                document.getElementById('preview-container').style.display = 'block';
                previewExcelData(data);
            });
        });

        // Event listener untuk import data
        document.getElementById('btn-import').addEventListener('click', function() {
            const fileInput = document.getElementById('file-import');
            const file = fileInput.files[0];
            
            if (!file) {
                alert('Pilih file Excel terlebih dahulu!');
                return;
            }
            
            readExcelFile(file, function(data) {
                const errors = validateStudentData(data);
                
                if (errors.length > 0) {
                    alert('Terjadi kesalahan dalam data:\n\n' + errors.join('\n'));
                    return;
                }
                
                if (confirm('Apakah Anda yakin ingin mengimport data siswa ini?')) {
                    const result = importStudentData(data);
                    alert(`Import selesai!\nBerhasil: ${result.imported} data\nDilewati: ${result.skipped} data`);
                    
                    // Update tabel siswa
                    updateTableSiswa();
                    
                    // Reset form
                    document.getElementById('file-import').value = '';
                    document.getElementById('preview-container').style.display = 'none';
                }
            });
        });

        // Event listener untuk konfirmasi import
        document.getElementById('btn-confirm-import').addEventListener('click', function() {
            const fileInput = document.getElementById('file-import');
            const file = fileInput.files[0];
            
            if (!file) {
                alert('Tidak ada file yang dipilih!');
                return;
            }
            
            readExcelFile(file, function(data) {
                const result = importStudentData(data);
                alert(`Import selesai!\nBerhasil: ${result.imported} data\nDilewati: ${result.skipped} data`);
                
                // Update tabel siswa
                updateTableSiswa();
                
                // Reset form
                document.getElementById('file-import').value = '';
                document.getElementById('preview-container').style.display = 'none';
            });
        });

        // Event listener untuk batal import
        document.getElementById('btn-cancel-import').addEventListener('click', function() {
            document.getElementById('preview-container').style.display = 'none';
            document.getElementById('file-import').value = '';
        });

        // Event listener untuk export laporan siswa
        document.getElementById('btn-export-siswa').addEventListener('click', function() {
            const data = getLaporanSiswaForExport();
            const filename = `laporan_pembayaran_siswa_${new Date().toISOString().split('T')[0]}.xlsx`;
            exportLaporanToExcel(data, filename, 'Laporan Siswa');
        });

        // Event listener untuk export laporan kelas
        document.getElementById('btn-export-kelas').addEventListener('click', function() {
            const data = getLaporanKelasForExport();
            const filename = `laporan_pembayaran_kelas_${new Date().toISOString().split('T')[0]}.xlsx`;
            exportLaporanToExcel(data, filename, 'Laporan Kelas');
        });

        // Event listener untuk export laporan tagihan
        document.getElementById('btn-export-tagihan').addEventListener('click', function() {
            const data = getLaporanTagihanForExport();
            const filename = `laporan_pembayaran_tagihan_${new Date().toISOString().split('T')[0]}.xlsx`;
            exportLaporanToExcel(data, filename, 'Laporan Tagihan');
        });

        // ==================== BACKUP & RESTORE ====================
        // Backup data
        document.getElementById('btn-backup').addEventListener('click', function() {
            const data = {
                siswa: getData('siswa'),
                tagihan: getData('tagihan'),
                pembayaran: getData('pembayaran'),
                backupDate: new Date().toISOString()
            };
            
            const dataStr = JSON.stringify(data, null, 2);
            const dataBlob = new Blob([dataStr], { type: 'application/json' });
            
            const url = URL.createObjectURL(dataBlob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `backup-pembayaran-${new Date().toISOString().split('T')[0]}.json`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            
            alert('Backup data berhasil!');
        });

        // Restore data
        document.getElementById('btn-restore').addEventListener('click', function() {
            const fileInput = document.getElementById('file-restore');
            const file = fileInput.files[0];
            
            if (!file) {
                alert('Pilih file backup terlebih dahulu!');
                return;
            }
            
            if (!confirm('PERINGATAN: Restore data akan menggantikan semua data yang ada saat ini. Lanjutkan?')) {
                return;
            }
            
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    
                    if (data.siswa && data.tagihan && data.pembayaran) {
                        saveData('siswa', data.siswa);
                        saveData('tagihan', data.tagihan);
                        saveData('pembayaran', data.pembayaran);
                        
                        // Update semua tampilan
                        updateTableSiswa();
                        updateTableTagihan();
                        updateTablePembayaran();
                        updateDashboard();
                        
                        alert('Restore data berhasil!');
                    } else {
                        alert('File backup tidak valid!');
                    }
                } catch (error) {
                    alert('Error membaca file backup: ' + error.message);
                }
            };
            reader.readAsText(file);
            
            // Reset input file
            fileInput.value = '';
        });

        // Reset data
        document.getElementById('btn-reset').addEventListener('click', function() {
            if (!confirm('PERINGATAN: Tindakan ini akan menghapus SEMUA data dan tidak dapat dibatalkan! Lanjutkan?')) {
                return;
            }
            
            if (!confirm('SANGAT YAKIN? Semua data siswa, tagihan, dan pembayaran akan dihapus permanen!')) {
                return;
            }
            
            // Hapus semua data
            localStorage.removeItem('siswa');
            localStorage.removeItem('tagihan');
            localStorage.removeItem('pembayaran');
            
            // Inisialisasi ulang
            initializeData();
            
            // Update semua tampilan
            updateTableSiswa();
            updateTableTagihan();
            updateTablePembayaran();
            updateDashboard();
            
            alert('Semua data telah direset!');
        });

        // ==================== UTILITY FUNCTIONS ====================
        // Update tanggal saat ini
        function updateCurrentDate() {
            const now = new Date();
            const options = { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            };
            document.getElementById('current-date').textContent = 
                now.toLocaleDateString('id-ID', options);
        }

        // Inisialisasi aplikasi
        function initApp() {
            initializeData();
            updateCurrentDate();
            updateTableSiswa();
            updateTableTagihan();
            updateTablePembayaran();
            updateDashboard();
            initializeAutocomplete();
            
            // Set tanggal pembayaran ke hari ini
            document.getElementById('tanggal-pembayaran').value = 
                new Date().toISOString().split('T')[0];
        }

        // Jalankan aplikasi saat halaman dimuat
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
