<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Pendaftaran Siswa Baru - SMKN 1 Probolinggo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
    <style>
        :root {
            --primary-color: #1e3a8a;
            --secondary-color: #3b82f6;
            --success-color: #10b981;
            --danger-color: #ef4444;
            --warning-color: #f59e0b;
        }

        body {
            background-color: #f3f4f6;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        .navbar {
            background-color: var(--primary-color) !important;
            box-shadow: 0 2px 4px rgba(0,0,0,.1);
        }

        .navbar-brand {
            font-weight: 600;
            font-size: 1.5rem;
        }

        .main-container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }

        .card {
            border: none;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.07);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .card:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
        }

        .card-header {
            background-color: var(--primary-color);
            color: white;
            border-radius: 12px 12px 0 0 !important;
            padding: 1.5rem;
            font-weight: 600;
        }

        .form-label {
            font-weight: 500;
            color: #374151;
            margin-bottom: 0.5rem;
        }

        .form-control, .form-select {
            border: 1px solid #d1d5db;
            border-radius: 8px;
            padding: 0.75rem;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        .form-control:focus, .form-select:focus {
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 0.2rem rgba(59, 130, 246, 0.25);
        }

        .btn-primary {
            background-color: var(--primary-color);
            border-color: var(--primary-color);
            border-radius: 8px;
            padding: 0.75rem 1.5rem;
            font-weight: 500;
            transition: all 0.2s;
        }

        .btn-primary:hover {
            background-color: #1e40af;
            border-color: #1e40af;
            transform: translateY(-1px);
        }

        .btn-success {
            background-color: var(--success-color);
            border-color: var(--success-color);
            border-radius: 8px;
            padding: 0.75rem 1.5rem;
            font-weight: 500;
        }

        .btn-warning {
            background-color: var(--warning-color);
            border-color: var(--warning-color);
            border-radius: 8px;
            padding: 0.75rem 1.5rem;
            font-weight: 500;
        }

        .btn-danger {
            background-color: var(--danger-color);
            border-color: var(--danger-color);
            border-radius: 8px;
            padding: 0.5rem 1rem;
            font-weight: 500;
        }

        .nav-pills .nav-link {
            border-radius: 8px;
            margin-right: 0.5rem;
            color: #6b7280;
            font-weight: 500;
        }

        .nav-pills .nav-link.active {
            background-color: var(--primary-color);
        }

        .table {
            border-radius: 8px;
            overflow: hidden;
        }

        .table thead {
            background-color: #f9fafb;
        }

        .badge {
            padding: 0.5rem 0.75rem;
            border-radius: 6px;
            font-weight: 500;
        }

        .preview-section {
            background-color: #f9fafb;
            border-radius: 8px;
            padding: 1.5rem;
            margin-top: 1rem;
        }

        .preview-item {
            display: flex;
            justify-content: space-between;
            padding: 0.5rem 0;
            border-bottom: 1px solid #e5e7eb;
        }

        .preview-item:last-child {
            border-bottom: none;
        }

        .preview-label {
            font-weight: 600;
            color: #4b5563;
        }

        .preview-value {
            color: #1f2937;
        }

        .stats-card {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-radius: 12px;
            padding: 1.5rem;
            margin-bottom: 1rem;
        }

        .stats-number {
            font-size: 2.5rem;
            font-weight: 700;
        }

        .stats-label {
            font-size: 0.875rem;
            opacity: 0.9;
        }

        .alert {
            border-radius: 8px;
            border: none;
        }

        .form-check-input:checked {
            background-color: var(--primary-color);
            border-color: var(--primary-color);
        }

        .loading-spinner {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 9999;
        }

        .toast-container {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 9999;
        }

        @media (max-width: 768px) {
            .main-container {
                margin: 1rem auto;
            }
            
            .stats-card {
                margin-bottom: 0.5rem;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Spinner -->
    <div class="loading-spinner">
        <div class="spinner-border text-primary" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>

    <!-- Toast Container -->
    <div class="toast-container"></div>

    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">
                <i class="bi bi-mortarboard-fill me-2"></i>
                SMKN 1 Probolinggo
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link active" href="#" onclick="showSection('form')">
                            <i class="bi bi-person-plus me-1"></i> Pendaftaran
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" onclick="showSection('data')">
                            <i class="bi bi-table me-1"></i> Data Siswa
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#" onclick="showSection('stats')">
                            <i class="bi bi-graph-up me-1"></i> Statistik
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Main Container -->
    <div class="main-container">
        <!-- Form Section -->
        <div id="formSection" class="section">
            <div class="row mb-4">
                <div class="col-12">
                    <h2 class="text-center mb-4">
                        <i class="bi bi-clipboard-data text-primary"></i>
                        Formulir Pendaftaran Siswa Baru
                    </h2>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <h5 class="mb-0">
                        <i class="bi bi-person-badge me-2"></i>
                        Data Pribadi Siswa
                    </h5>
                </div>
                <div class="card-body">
                    <form id="studentForm">
                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="namaLengkap" class="form-label">Nama Lengkap <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="namaLengkap" required>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="nisn" class="form-label">NISN <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="nisn" pattern="[0-9]{10}" maxlength="10" required>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="tempatLahir" class="form-label">Tempat Lahir <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="tempatLahir" required>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="tanggalLahir" class="form-label">Tanggal Lahir <span class="text-danger">*</span></label>
                                <input type="date" class="form-control" id="tanggalLahir" required>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="jenisKelamin" class="form-label">Jenis Kelamin <span class="text-danger">*</span></label>
                                <select class="form-select" id="jenisKelamin" required>
                                    <option value="">Pilih Jenis Kelamin</option>
                                    <option value="Laki-laki">Laki-laki</option>
                                    <option value="Perempuan">Perempuan</option>
                                </select>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="agama" class="form-label">Agama <span class="text-danger">*</span></label>
                                <select class="form-select" id="agama" required>
                                    <option value="">Pilih Agama</option>
                                    <option value="Islam">Islam</option>
                                    <option value="Kristen">Kristen</option>
                                    <option value="Katolik">Katolik</option>
                                    <option value="Hindu">Hindu</option>
                                    <option value="Buddha">Buddha</option>
                                    <option value="Konghucu">Konghucu</option>
                                </select>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="alamat" class="form-label">Alamat Lengkap <span class="text-danger">*</span></label>
                                <textarea class="form-control" id="alamat" rows="2" required></textarea>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="noHp" class="form-label">Nomor HP <span class="text-danger">*</span></label>
                                <input type="tel" class="form-control" id="noHp" pattern="[0-9]{10,13}" required>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="email" class="form-label">Email <span class="text-danger">*</span></label>
                                <input type="email" class="form-control" id="email" required>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="asalSekolah" class="form-label">Asal Sekolah <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="asalSekolah" required>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h5 class="mb-0">
                            <i class="bi bi-people me-2"></i>
                            Data Orang Tua/Wali
                        </h5>
                    </div>
                    <div class="card-body">
                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="namaAyah" class="form-label">Nama Ayah <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="namaAyah" required>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="pekerjaanAyah" class="form-label">Pekerjaan Ayah <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="pekerjaanAyah" required>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="namaIbu" class="form-label">Nama Ibu <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="namaIbu" required>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="pekerjaanIbu" class="form-label">Pekerjaan Ibu <span class="text-danger">*</span></label>
                                <input type="text" class="form-control" id="pekerjaanIbu" required>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="noHpOrtu" class="form-label">Nomor HP Orang Tua <span class="text-danger">*</span></label>
                                <input type="tel" class="form-control" id="noHpOrtu" pattern="[0-9]{10,13}" required>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="penghasilan" class="form-label">Penghasilan Orang Tua <span class="text-danger">*</span></label>
                                <select class="form-select" id="penghasilan" required>
                                    <option value="">Pilih Penghasilan</option>
                                    <option value="< 1 juta">< Rp 1.000.000</option>
                                    <option value="1-3 juta">Rp 1.000.000 - 3.000.000</option>
                                    <option value="3-5 juta">Rp 3.000.000 - 5.000.000</option>
                                    <option value="> 5 juta">> Rp 5.000.000</option>
                                </select>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h5 class="mb-0">
                            <i class="bi bi-book me-2"></i>
                            Pilihan Jurusan
                        </h5>
                    </div>
                    <div class="card-body">
                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <label for="pilihan1" class="form-label">Pilihan Jurusan 1 <span class="text-danger">*</span></label>
                                <select class="form-select" id="pilihan1" required>
                                    <option value="">Pilih Jurusan</option>
                                    <option value="Teknik Komputer dan Jaringan">Teknik Komputer dan Jaringan</option>
                                    <option value="Rekayasa Perangkat Lunak">Rekayasa Perangkat Lunak</option>
                                    <option value="Multimedia">Multimedia</option>
                                    <option value="Akuntansi">Akuntansi</option>
                                    <option value="Administrasi Perkantoran">Administrasi Perkantoran</option>
                                    <option value="Pemasaran">Pemasaran</option>
                                    <option value="Tata Boga">Tata Boga</option>
                                    <option value="Tata Busana">Tata Busana</option>
                                </select>
                            </div>
                            <div class="col-md-6 mb-3">
                                <label for="pilihan2" class="form-label">Pilihan Jurusan 2</label>
                                <select class="form-select" id="pilihan2">
                                    <option value="">Pilih Jurusan</option>
                                    <option value="Teknik Komputer dan Jaringan">Teknik Komputer dan Jaringan</option>
                                    <option value="Rekayasa Perangkat Lunak">Rekayasa Perangkat Lunak</option>
                                    <option value="Multimedia">Multimedia</option>
                                    <option value="Akuntansi">Akuntansi</option>
                                    <option value="Administrasi Perkantoran">Administrasi Perkantoran</option>
                                    <option value="Pemasaran">Pemasaran</option>
                                    <option value="Tata Boga">Tata Boga</option>
                                    <option value="Tata Busana">Tata Busana</option>
                                </select>
                            </div>
                        </div>

                        <div class="mb-3">
                            <label for="alasan" class="form-label">Alasan Memilih Jurusan</label>
                            <textarea class="form-control" id="alasan" rows="3" placeholder="Jelaskan alasan Anda memilih jurusan tersebut..."></textarea>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h5 class="mb-0">
                            <i class="bi bi-file-earmark-text me-2"></i>
                            Dokumen Pendukung
                        </h5>
                    </div>
                    <div class="card-body">
                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" id="ijazah" required>
                                    <label class="form-check-label" for="ijazah">
                                        Fotokopi Ijazah/SKL
                                    </label>
                                </div>
                            </div>
                            <div class="col-md-6 mb-3">
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" id="kk" required>
                                    <label class="form-check-label" for="kk">
                                        Fotokopi Kartu Keluarga
                                    </label>
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" id="akta" required>
                                    <label class="form-check-label" for="akta">
                                        Fotokopi Akta Kelahiran
                                    </label>
                                </div>
                            </div>
                            <div class="col-md-6 mb-3">
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" id="pasfoto" required>
                                    <label class="form-check-label" for="pasfoto">
                                        Pas Foto 3x4 (3 lembar)
                                    </label>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-body">
                        <div class="d-flex justify-content-between">
                            <button type="button" class="btn btn-warning" onclick="resetForm()">
                                <i class="bi bi-arrow-clockwise me-1"></i> Reset Form
                            </button>
                            <button type="button" class="btn btn-primary" onclick="previewData()">
                                <i class="bi bi-eye me-1"></i> Preview Data
                            </button>
                        </div>
                    </div>
                </div>
            </form>
        </div>

        <!-- Preview Modal -->
        <div class="modal fade" id="previewModal" tabindex="-1">
            <div class="modal-dialog modal-lg">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title">
                            <i class="bi bi-eye me-2"></i>Preview Data Pendaftaran
                        </h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                    </div>
                    <div class="modal-body" id="previewContent">
                        <!-- Preview content will be inserted here -->
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Edit</button>
                        <button type="button" class="btn btn-success" onclick="submitForm()">
                            <i class="bi bi-check-circle me-1"></i> Konfirmasi & Simpan
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Data Section -->
        <div id="dataSection" class="section" style="display: none;">
            <div class="row mb-4">
                <div class="col-12">
                    <h2 class="text-center mb-4">
                        <i class="bi bi-table text-primary"></i>
                        Data Siswa Terdaftar
                    </h2>
                </div>
            </div>

            <div class="card">
                <div class="card-body">
                    <div class="row mb-3">
                        <div class="col-md-6">
                            <div class="input-group">
                                <span class="input-group-text"><i class="bi bi-search"></i></span>
                                <input type="text" class="form-control" id="searchInput" placeholder="Cari nama atau NISN...">
                            </div>
                        </div>
                        <div class="col-md-6">
                            <select class="form-select" id="filterJurusan">
                                <option value="">Semua Jurusan</option>
                                <option value="Teknik Komputer dan Jaringan">Teknik Komputer dan Jaringan</option>
                                <option value="Rekayasa Perangkat Lunak">Rekayasa Perangkat Lunak</option>
                                <option value="Multimedia">Multimedia</option>
                                <option value="Akuntansi">Akuntansi</option>
                                <option value="Administrasi Perkantoran">Administrasi Perkantoran</option>
                                <option value="Pemasaran">Pemasaran</option>
                                <option value="Tata Boga">Tata Boga</option>
                                <option value="Tata Busana">Tata Busana</option>
                            </select>
                        </div>
                    </div>

                    <div class="table-responsive">
                        <table class="table table-hover">
                            <thead>
                                <tr>
                                    <th>No</th>
                                    <th>Nama</th>
                                    <th>NISN</th>
                                    <th>Jurusan Pilihan 1</th>
                                    <th>Jenis Kelamin</th>
                                    <th>Status</th>
                                    <th>Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="studentTableBody">
                                <!-- Data will be inserted here -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- Stats Section -->
        <div id="statsSection" class="section" style="display: none;">
            <div class="row mb-4">
                <div class="col-12">
                    <h2 class="text-center mb-4">
                        <i class="bi bi-graph-up text-primary"></i>
                        Statistik Pendaftaran
                    </h2>
                </div>
            </div>

            <div class="row">
                <div class="col-md-3 col-sm-6 mb-3">
                    <div class="stats-card">
                        <div class="stats-number" id="totalPendaftar">0</div>
                        <div class="stats-label">Total Pendaftar</div>
                    </div>
                </div>
                <div class="col-md-3 col-sm-6 mb-3">
                    <div class="stats-card">
                        <div class="stats-number" id="totalLaki">0</div>
                        <div class="stats-label">Laki-laki</div>
                    </div>
                </div>
                <div class="col-md-3 col-sm-6 mb-3">
                    <div class="stats-card">
                        <div class="stats-number" id="totalPerempuan">0</div>
                        <div class="stats-label">Perempuan</div>
                    </div>
                </div>
                <div class="col-md-3 col-sm-6 mb-3">
                    <div class="stats-card">
                        <div class="stats-number" id="todayPendaftar">0</div>
                        <div class="stats-label">Pendaftar Hari Ini</div>
                    </div>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <h5 class="mb-0">
                        <i class="bi bi-bar-chart me-2"></i>
                        Distribusi Jurusan
                    </h5>
                </div>
                <div class="card-body">
                    <canvas id="jurusanChart" width="400" height="200"></canvas>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        // Global variables
        let students = JSON.parse(localStorage.getItem('students')) || [];
        let currentSection = 'form';
        let jurusanChart = null;

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            updateStudentTable();
            updateStats();
            initializeEventListeners();
        });

        // Initialize event listeners
        function initializeEventListeners() {
            document.getElementById('searchInput').addEventListener('input', filterTable);
            document.getElementById('filterJurusan').addEventListener('change', filterTable);
        }

        // Show section
        function showSection(section) {
            document.querySelectorAll('.section').forEach(s => s.style.display = 'none');
            document.getElementById(section + 'Section').style.display = 'block';
            
            // Update navbar active state
            document.querySelectorAll('.navbar-nav .nav-link').forEach(link => {
                link.classList.remove('active');
            });
            event.target.classList.add('active');
            
            currentSection = section;
            
            if (section === 'stats') {
                updateStats();
                updateJurusanChart();
            }
        }

        // Preview data
        function previewData() {
            const formData = getFormData();
            
            if (!validateForm(formData)) {
                showToast('Harap lengkapi semua field yang wajib diisi!', 'warning');
                return;
            }
            
            const previewContent = generatePreviewHTML(formData);
            document.getElementById('previewContent').innerHTML = previewContent;
            
            const modal = new bootstrap.Modal(document.getElementById('previewModal'));
            modal.show();
        }

        // Get form data
        function getFormData() {
            return {
                namaLengkap: document.getElementById('namaLengkap').value,
                nisn: document.getElementById('nisn').value,
                tempatLahir: document.getElementById('tempatLahir').value,
                tanggalLahir: document.getElementById('tanggalLahir').value,
                jenisKelamin: document.getElementById('jenisKelamin').value,
                agama: document.getElementById('agama').value,
                alamat: document.getElementById('alamat').value,
                noHp: document.getElementById('noHp').value,
                email: document.getElementById('email').value,
                asalSekolah: document.getElementById('asalSekolah').value,
                namaAyah: document.getElementById('namaAyah').value,
                pekerjaanAyah: document.getElementById('pekerjaanAyah').value,
                namaIbu: document.getElementById('namaIbu').value,
                pekerjaanIbu: document.getElementById('pekerjaanIbu').value,
                noHpOrtu: document.getElementById('noHpOrtu').value,
                penghasilan: document.getElementById('penghasilan').value,
                pilihan1: document.getElementById('pilihan1').value,
                pilihan2: document.getElementById('pilihan2').value,
                alasan: document.getElementById('alasan').value,
                tanggalDaftar: new Date().toISOString()
            };
        }

        // Validate form
        function validateForm(data) {
            const requiredFields = [
                'namaLengkap', 'nisn', 'tempatLahir', 'tanggalLahir', 
                'jenisKelamin', 'agama', 'alamat', 'noHp', 'email', 
                'asalSekolah', 'namaAyah', 'pekerjaanAyah', 'namaIbu', 
                'pekerjaanIbu', 'noHpOrtu', 'penghasilan', 'pilihan1'
            ];
            
            const checkboxes = ['ijazah', 'kk', 'akta', 'pasfoto'];
            
            for (let field of requiredFields) {
                if (!data[field] || data[field].trim() === '') {
                    return false;
                }
            }
            
            for (let checkbox of checkboxes) {
                if (!document.getElementById(checkbox).checked) {
                    return false;
                }
            }
            
            return true;
        }

        // Generate preview HTML
        function generatePreviewHTML(data) {
            return `
                <div class="preview-section">
                    <h6 class="mb-3"><i class="bi bi-person me-2"></i>Data Pribadi</h6>
                    <div class="preview-item">
                        <span class="preview-label">Nama Lengkap:</span>
                        <span class="preview-value">${data.namaLengkap}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">NISN:</span>
                        <span class="preview-value">${data.nisn}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Tempat, Tanggal Lahir:</span>
                        <span class="preview-value">${data.tempatLahir}, ${formatDate(data.tanggalLahir)}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Jenis Kelamin:</span>
                        <span class="preview-value">${data.jenisKelamin}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Agama:</span>
                        <span class="preview-value">${data.agama}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Alamat:</span>
                        <span class="preview-value">${data.alamat}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">No. HP:</span>
                        <span class="preview-value">${data.noHp}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Email:</span>
                        <span class="preview-value">${data.email}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Asal Sekolah:</span>
                        <span class="preview-value">${data.asalSekolah}</span>
                    </div>
                </div>
                
                <div class="preview-section mt-3">
                    <h6 class="mb-3"><i class="bi bi-people me-2"></i>Data Orang Tua</h6>
                    <div class="preview-item">
                        <span class="preview-label">Nama Ayah:</span>
                        <span class="preview-value">${data.namaAyah}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Pekerjaan Ayah:</span>
                        <span class="preview-value">${data.pekerjaanAyah}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Nama Ibu:</span>
                        <span class="preview-value">${data.namaIbu}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Pekerjaan Ibu:</span>
                        <span class="preview-value">${data.pekerjaanIbu}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">No. HP Orang Tua:</span>
                        <span class="preview-value">${data.noHpOrtu}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Penghasilan:</span>
                        <span class="preview-value">${data.penghasilan}</span>
                    </div>
                </div>
                
                <div class="preview-section mt-3">
                    <h6 class="mb-3"><i class="bi bi-book me-2"></i>Pilihan Jurusan</h6>
                    <div class="preview-item">
                        <span class="preview-label">Pilihan 1:</span>
                        <span class="preview-value">${data.pilihan1}</span>
                    </div>
                    <div class="preview-item">
                        <span class="preview-label">Pilihan 2:</span>
                        <span class="preview-value">${data.pilihan2 || '-'}</span>
                    </div>
                    ${data.alasan ? `
                    <div class="preview-item">
                        <span class="preview-label">Alasan:</span>
                        <span class="preview-value">${data.alasan}</span>
                    </div>
                    ` : ''}
                </div>
            `;
        }

        // Submit form
        function submitForm() {
            const formData = getFormData();
            
            // Add ID and status
            formData.id = Date.now();
            formData.status = 'Terdaftar';
            
            // Save to localStorage
            students.push(formData);
            localStorage.setItem('students', JSON.stringify(students));
            
            // Close modal
            bootstrap.Modal.getInstance(document.getElementById('previewModal')).hide();
            
            // Reset form
            resetForm();
            
            // Show success message
            showToast('Data siswa berhasil disimpan!', 'success');
            
            // Update table and stats
            updateStudentTable();
            updateStats();
        }

        // Reset form
        function resetForm() {
            document.getElementById('studentForm').reset();
            document.querySelectorAll('.form-check-input').forEach(cb => cb.checked = false);
        }

        // Update student table
        function updateStudentTable() {
            const tbody = document.getElementById('studentTableBody');
            tbody.innerHTML = '';
            
            students.forEach((student, index) => {
                const row = `
                    <tr>
                        <td>${index + 1}</td>
                        <td>${student.namaLengkap}</td>
                        <td>${student.nisn}</td>
                        <td>${student.pilihan1}</td>
                        <td>${student.jenisKelamin}</td>
                        <td>
                            <span class="badge bg-success">${student.status}</span>
                        </td>
                        <td>
                            <button class="btn btn-sm btn-primary" onclick="viewStudent(${student.id})">
                                <i class="bi bi-eye"></i>
                            </button>
                            <button class="btn btn-sm btn-danger" onclick="deleteStudent(${student.id})">
                                <i class="bi bi-trash"></i>
                            </button>
                        </td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });
        }

        // Filter table
        function filterTable() {
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const filterJurusan = document.getElementById('filterJurusan').value;
            
            const rows = document.querySelectorAll('#studentTableBody tr');
            
            rows.forEach(row => {
                const nama = row.cells[1].textContent.toLowerCase();
                const nisn = row.cells[2].textContent.toLowerCase();
                const jurusan = row.cells[3].textContent;
                
                const matchSearch = nama.includes(searchTerm) || nisn.includes(searchTerm);
                const matchJurusan = !filterJurusan || jurusan === filterJurusan;
                
                row.style.display = matchSearch && matchJurusan ? '' : 'none';
            });
        }

        // View student details
        function viewStudent(id) {
            const student = students.find(s => s.id === id);
            if (student) {
                const previewContent = generatePreviewHTML(student);
                document.getElementById('previewContent').innerHTML = previewContent;
                
                const modal = new bootstrap.Modal(document.getElementById('previewModal'));
                modal.show();
                
                // Hide submit button in view mode
                modal._element.querySelector('.btn-success').style.display = 'none';
            }
        }

        // Delete student
        function deleteStudent(id) {
            if (confirm('Apakah Anda yakin ingin menghapus data siswa ini?')) {
                students = students.filter(s => s.id !== id);
                localStorage.setItem('students', JSON.stringify(students));
                
                updateStudentTable();
                updateStats();
                
                showToast('Data siswa berhasil dihapus!', 'success');
            }
        }

        // Update statistics
        function updateStats() {
            const total = students.length;
            const laki = students.filter(s => s.jenisKelamin === 'Laki-laki').length;
            const perempuan = students.filter(s => s.jenisKelamin === 'Perempuan').length;
            
            const today = new Date().toDateString();
            const todayCount = students.filter(s => {
                const daftarDate = new Date(s.tanggalDaftar).toDateString();
                return daftarDate === today;
            }).length;
            
            document.getElementById('totalPendaftar').textContent = total;
            document.getElementById('totalLaki').textContent = laki;
            document.getElementById('totalPerempuan').textContent = perempuan;
            document.getElementById('todayPendaftar').textContent = todayCount;
        }

        // Update jurusan chart
        function updateJurusanChart() {
            const ctx = document.getElementById('jurusanChart').getContext('2d');
            
            // Count students per jurusan
            const jurusanCount = {};
            students.forEach(student => {
                jurusanCount[student.pilihan1] = (jurusanCount[student.pilihan1] || 0) + 1;
            });
            
            const labels = Object.keys(jurusanCount);
            const data = Object.values(jurusanCount);
            
            if (jurusanChart) {
                jurusanChart.destroy();
            }
            
            jurusanChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Jumlah Pendaftar',
                        data: data,
                        backgroundColor: 'rgba(59, 130, 246, 0.5)',
                        borderColor: 'rgba(59, 130, 246, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                stepSize: 1
                            }
                        }
                    }
                }
            });
        }

        // Format date
        function formatDate(dateString) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            return new Date(dateString).toLocaleDateString('id-ID', options);
        }

        // Show toast notification
        function showToast(message, type = 'info') {
            const toastContainer = document.querySelector('.toast-container');
            const toastId = 'toast-' + Date.now();
            
            const toastHTML = `
                <div id="${toastId}" class="toast align-items-center text-white bg-${type === 'success' ? 'success' : type === 'warning' ? 'warning' : 'primary'} border-0" role="alert">
                    <div class="d-flex">
                        <div class="toast-body">
                            ${message}
                        </div>
                        <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
                    </div>
                </div>
            `;
            
            toastContainer.insertAdjacentHTML('beforeend', toastHTML);
            
            const toastElement = document.getElementById(toastId);
            const toast = new bootstrap.Toast(toastElement);
            toast.show();
            
            toastElement.addEventListener('hidden.bs.toast', () => {
                toastElement.remove();
            });
        }
    </script>
</body>
</html>
