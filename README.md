# UAS_SIM
Sistem Informasi Managemen
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kuis Interaktif UAS</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(to right, #a8dadc 0%, #457b9d 100%); /* Biru pastel lembut */
            color: #333; /* Warna teks lebih gelap untuk kontras */
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
        }

        .quiz-container {
            background-color: #f1faee; /* Krem pastel */
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15); /* Bayangan lebih lembut */
            width: 100%;
            max-width: 900px;
            color: #333;
            text-align: center;
            animation: fadeIn 1s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 {
            color: #e63946; /* Merah muda pastel */
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.05); /* Text shadow lebih halus */
        }

        .question-section {
            text-align: left;
            margin-bottom: 25px;
            padding: 20px;
            background-color: #fff; /* Putih */
            border-radius: 10px;
            border-left: 5px solid #f4a261; /* Oranye pastel */
            transition: all 0.3s ease;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.08); /* Bayangan lebih kecil */
        }

        .question-section:hover {
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .question-text {
            font-size: 1.2em;
            margin-bottom: 15px;
            color: #333;
            line-height: 1.6;
        }

        .options-container label {
            display: block;
            background-color: #e0fbfc; /* Biru muda pastel */
            padding: 12px 20px;
            margin-bottom: 10px;
            border-radius: 8px;
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.2s ease;
            font-size: 1.1em;
            color: #555;
            display: flex;
            align-items: center;
        }

        .options-container label:hover {
            background-color: #b7e4c7; /* Hijau muda pastel */
            transform: translateX(5px);
        }

        .options-container input,
        .options-container label {
            /* Menjaga agar input dan label sejajar */
            vertical-align: middle;
        }

        .options-container input::before {
            /* Membuat lingkaran radio button kustom (opsional) */
            content: '';
            display: inline-block;
            width: 1em;
            height: 1em;
            border-radius: 50%;
            border: 1px solid #777;
            margin-right: 10px;
            vertical-align: middle;
        }

        .options-container input:checked::before {
            background-color: #a8dadc; /* Warna aktif radio button */
            border-color: #457b9d;
            padding: 0.2em;
        }

        .options-container input {
            /* Menyembunyikan radio button asli */
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            margin: 0; /* Reset margin */
        }

        .submit-btn, .retry-btn {
            background-color: #8ac926; /* Hijau pastel cerah */
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.3em;
            margin-top: 30px;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Bayangan lebih halus */
        }

        .submit-btn:hover {
            background-color: #6a994e; /* Hijau pastel lebih gelap */
            transform: translateY(-3px);
        }

        .retry-btn {
            background-color: #f72585; /* Pink pastel */
        }

        .retry-btn:hover {
            background-color: #b5179e; /* Pink pastel lebih gelap */
            transform: translateY(-3px);
        }

        .results-container {
            margin-top: 40px;
            padding: 30px;
            background-color: #d4edda; /* Hijau sangat muda pastel */
            border-radius: 10px;
            color: #1b4332; /* Hijau gelap pastel */
            font-size: 1.5em;
            font-weight: bold;
            display: none; /* Hidden by default */
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .score {
            font-size: 2em;
            color: #457b9d; /* Biru pastel */
            margin-top: 15px;
        }

        .correct-answer {
            background-color: #ccf381 !important; /* Hijau terang pastel */
            border-left-color: #47b39c !important; /* Hijau toska pastel */
            font-weight: bold;
            color: #184e77 !important; /* Biru gelap pastel */
        }

        .incorrect-answer {
            background-color: #ffdde1 !important; /* Merah muda sangat muda pastel */
            border-left-color: #e29587 !important; /* Oranye kemerahan pastel */
            color: #2b2c28 !important; /* Abu-abu gelap */
        }

        .feedback {
            margin-top: 10px;
            font-size: 0.9em;
            color: #6c757d;
        }

        .question-section.correct {
            border-color: #47b39c;
            background-color: #e7f6f2; /* Hijau sangat muda */
        }

        .question-section.incorrect {
            border-color: #e29587;
            background-color: #fef6e4; /* Krem muda */
        }

        /* Responsive adjustments for smaller screens */
        @media (max-width: 768px) {
            body {
                padding: 10px;
            }

            .quiz-container {
                padding: 20px;
                border-radius: 10px;
                box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
            }

            h1 {
                font-size: 2em;
                margin-bottom: 20px;
            }

            .question-section {
                padding: 15px;
                margin-bottom: 20px;
            }

            .question-text {
                font-size: 1em;
                margin-bottom: 10px;
            }

            .options-container label {
                padding: 10px 15px;
                font-size: 1em;
            }

            .options-container input::before {
                width: 0.9em;
                height: 0.9em;
                margin-right: 8px;
            }

            .submit-btn, .retry-btn {
                padding: 12px 25px;
                font-size: 1.1em;
                margin-top: 20px;
            }

            .results-container {
                padding: 20px;
                font-size: 1.2em;
                margin-top: 20px;
            }

            .score {
                font-size: 1.8em;
            }
        }

        @media (max-width: 480px) {
            .quiz-container {
                padding: 15px;
            }

            h1 {
                font-size: 1.8em;
                margin-bottom: 15px;
            }

            .question-text {
                font-size: 0.95em;
            }

            .options-container label {
                font-size: 0.95em;
                padding: 8px 12px;
            }

            .submit-btn, .retry-btn {
                font-size: 1em;
                padding: 10px 20px;
            }

            .results-container {
                font-size: 1em;
                padding: 15px;
            }

            .score {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>Kuis Ujian Akhir Semester</h1>
        <form id="quizForm">
            </form>
        <button type="button" class="submit-btn" onclick="submitQuiz()">Selesai Ujian</button>
        <div id="results" class="results-container">
            <h2>Hasil Ujian Anda:</h2>
            <p>Anda mendapatkan <span id="score">0</span> dari 50 pertanyaan.</p>
            <button type="button" class="retry-btn" onclick="resetQuiz()">Ulangi Ujian</button>
        </div>
    </div>

    <script>
        const allQuestions = [
            {
                question: "Fungsi sistem informasi adalah mengubah data menjadi ....",
                options: ["informasi", "informatika", "keputusan", "kebutuhan"],
                correct: "informasi"
            },
            {
                question: "Infrastruktur teknologi informasi guna berbagi data disebut ....",
                options: ["perangkat keras", "perangkat lunak", "perangkat telekomunikasi", "penyimpanan data"],
                correct: "perangkat telekomunikasi"
            },
            {
                question: "Tiga level hirarki organisasi yang umum dijumpai pada berbagai perusahaan adalah ....",
                options: ["manajemen puncak, manajemen operasional, pekerja", "manajemen puncak, manajemen menengah, manajemen operasional", "manajemen puncak, manajemen operasional, sistem informasi", "manajemen puncak, manajemen menengah, pekerja"],
                correct: "manajemen puncak, manajemen menengah, manajemen operasional"
            },
            {
                question: "Point of sales yang mengolah data penjualan termasuk dalam tipe sistem informasi ....",
                options: ["sistem pembuatan keputusan", "sistem pemrosesan transaksi", "sistem pakar", "sistem penjualan"],
                correct: "sistem pemrosesan transaksi"
            },
            {
                question: "Sistem terdiri dari komponen yang sering disebut sebagai ....",
                options: ["subsistem", "supra sistem", "sub sistem", "sistemik"],
                correct: "subsistem"
            },
            {
                question: "Informasi dibutuhkan guna membuat keputusan yang ....",
                options: ["maksimal", "optimal", "rasional", "bilingual"],
                correct: "optimal"
            },
            {
                question: "Orang yang bertanggung jawab untuk menentukan arah dan tujuan suatu perusahaan adalah ....",
                options: ["manajer menengah", "supervisor", "mandor", "manajer puncak"],
                correct: "manajer puncak"
            },
            {
                question: "Operasi rutin harian suatu perusahaan merupakan tanggung jawab dari manajer ....",
                options: ["Operasional", "umum", "puncak", "HRD"],
                correct: "Operasional"
            },
            {
                question: "Regulasi yang dikembangkan oleh suatu perusahaan guna menyelesaikan atau melaksanakan suatu tugas disebut proses ....",
                options: ["manual", "otomatis", "bisnis", "digital"],
                correct: "bisnis"
            },
            {
                question: "Kumpulan instruksi yang digunakan untuk mengendalikan dan mengkoordinasikan sebuah komputer disebut perangkat ....",
                options: ["cadangan", "catu daya", "keras", "lunak"],
                correct: "lunak"
            },
            {
                question: "Munculnya layanan streaming film dan musik merupakan perkembangan bisnis berbasis teknologi informasi dalam bentuk ....",
                options: ["model usaha baru", "proses bisnis baru", "strategi usaha baru", "pendapatan baru"],
                correct: "model usaha baru"
            },
            {
                question: "Internet memungkinkan pengusaha UMKM di Indonesia berjualan ke luar negeri dengan cara menurunkan biaya ....",
                options: ["upah dan gaji", "produksi", "operasional", "tak terduga"],
                correct: "operasional"
            },
            {
                question: "Keunikan barang digital dibandingkan dengan barang konvensional adalah ....",
                options: ["biaya pemasaran sangat tinggi", "keuntungan pasti besar", "profit margin rendah", "biaya produksi hanya sebesar biaya produksi unit pertama"],
                correct: "biaya produksi hanya sebesar biaya produksi unit pertama"
            },
            {
                question: "Biaya untuk berpindah ke penjual lain bagi seorang konsumen disebut sebagai ....",
                options: ["switching cost", "variable cost", "fixed cost", "shared cost"],
                correct: "switching cost"
            },
            {
                question: "Kualitas informasi ketepatan waktu biasanya berbanding terbalik dengan ....",
                options: ["ketersediaan akses", "kelengkapan", "kehandalan", "kepercayaan"],
                correct: "kelengkapan"
            },
            {
                question: "Mesin Anjungan Tunai Mandiri merupakan contoh teknologi informasi yang berguna untuk ....",
                options: ["meraih keuntungan besar", "keunggulan kompetitif", "bertahan hidup", "keunggulan non kompetitif"],
                correct: "bertahan hidup"
            },
            {
                question: "Perkembangan teknologi yang secara drastis mengubah tatanan usaha di berbagai industri disebut sebagai ....",
                options: ["teknologi unggul", "adopsi teknologi", "difusi teknologi", "disrupsi teknologi"],
                correct: "disrupsi teknologi"
            },
            {
                question: "Aplikasi yang memungkinkan suatu mesin dikendalikan melalui internet disebut sebagai ....",
                options: ["Internet of Things", "Internet version 2.0", "Semantic web", "Intelligent Web"],
                correct: "Internet of Things"
            },
            {
                question: "Kemampuan untuk menemukan keterkaitan antara data yang nampak tidak saling berhubungan merupakan kelebihan dari teknologi ....",
                options: ["Google SEO", "Big Data", "Business Reengineering", "Business Rendering"],
                correct: "Big Data"
            },
            {
                question: "BRI membeli dan mengoperasikan sendiri satelit telekomunikasi dengan tujuan untuk mengatasi masalah ....",
                options: ["jaringan telekomunikasi", "distribusi dana nasabah", "kredit macet", "fraud perbankan"],
                correct: "jaringan telekomunikasi"
            },
            {
                question: "Pendekatan yang menggunakan dasar ilmu teknik adalah ....",
                options: ["hard approach", "soft approach", "technical approach", "social approach"],
                correct: "hard approach"
            },
            {
                question: "Pendekatan yang berfokus pada aspek perilaku para pengguna sistem informasi adalah ....",
                options: ["hard approach", "soft approach", "technical approach", "social approach"],
                correct: "soft approach"
            },
            {
                question: "Pendekatan yang menggabungkan pendekatan teknis dan perilaku adalah ....",
                options: ["hard approach", "soft approach", "technical approach", "socio-technical approach"],
                correct: "socio-technical approach"
            },
            {
                question: "Ilmu yang mempelajari dasar matematis teknologi informasi adalah Ilmu ....",
                options: ["Aljabar", "Rekayasa", "Matematika Dasar", "Komputer"],
                correct: "Komputer"
            },
            {
                question: "Ilmu yang mempelajari cara pembuatan keputusan manajerial secara ilmiah adalah ....",
                options: ["Manajemen Operasional", "Manajemen Sains", "Manajemen Keuangan", "Manajemen Strategis"],
                correct: "Manajemen Sains"
            },
            {
                question: "Ilmu yang mempelajari perilaku individu dalam menggunakan sebuah sistem informasi adalah ....",
                options: ["psikologi", "Para Psikologi", "kognisi", "meta Kognisi"],
                correct: "psikologi"
            },
            {
                question: "Jika kita mempelajari dampak gawai terhadap suasana kerja, maka kita menggunakan dasar ilmu ....",
                options: ["Sosiatri", "Antropologi", "sosiologi", "Ekonomi"],
                correct: "sosiologi"
            },
            {
                question: "Jika kita menghitung harga jual paket berlangganan streaming layanan musik seperti Spotify dan Joox, maka kita menggunakan dasar ilmu ....",
                options: ["Sosiatri", "Antropologi", "sosiologi", "Ekonomi"],
                correct: "Ekonomi"
            },
            {
                question: "Menunda penggunaan gawai terbaru di suatu perusahaan karena menunggu pelatihan karyawan merupakan contoh penggunaan pendekatan ....",
                options: ["hard approach", "soft approach", "technical approach", "socio-technical approach"],
                correct: "socio-technical approach"
            },
            {
                question: "Menghitung pendayagunaan fasilitas komputasi perusahaan secara optimal merupakan fokus bidang ilmu .....",
                options: ["Manajemen Operasional", "Operations Research", "Manajemen Keuangan", "Manajemen Strategis"],
                correct: "Operations Research"
            },
            {
                question: "Menerima pesanan dari konsumen merupakan proses bisnis dalam fungsi ....",
                options: ["penjualan dan pemasaran", "akuntansi dan keuangan", "produksi dan manufaktur", "sumber daya manusia"],
                correct: "penjualan dan pemasaran"
            },
            {
                question: "Berdagang melalui internet disebut sebagai aktivitas ....",
                options: ["E-Government", "E-catalogue", "E-Procurement", "E-commerce"],
                correct: "E-commerce"
            },
            {
                question: "Penggunaan E-Business untuk bertransaksi antara pemerintah dengan penyedia jasa konstruksi masuk ke dalam kategori ....",
                options: ["E-Business", "E-Government", "E-voting", "E-Commerce"],
                correct: "E-Government"
            },
            {
                question: "Perangkat teknologi informasi yang berguna untuk membantu kolaborasi antara lain adalah ....",
                options: ["ERP", "ECM", "Email", "E-catalogue"],
                correct: "Email"
            },
            {
                question: "Orang yang bertanggung jawab untuk membuat aplikasi adalah ....",
                options: ["programmer", "controller", "systems administrator", "designer"],
                correct: "programmer"
            },
            {
                question: "Bekerja sama dengan orang lain untuk mencapai tujuan bersama merupakan definisi dari ....",
                options: ["kolaborasi", "koordinasi", "kooperasi", "kooptasi"],
                correct: "kolaborasi"
            },
            {
                question: "Sistem yang digunakan untuk mengelola pengetahuan dalam perusahaan disebut ....",
                options: ["knowledge sharing", "Knowledge management systems", "Knowledge distribution", "Knowledge factory"],
                correct: "Knowledge management systems"
            },
            {
                question: "Sistem informasi fungsional yang tidak terintegrasi akan menciptakan fenomena ....",
                options: ["disfungsonalisasi informasi", "disintegrasi informasi", "silo informasi", "disintermediasi informasi"],
                correct: "silo informasi"
            },
            {
                question: "Sistem yang dirancang untuk membantu pembuatan keputusan semi terstruktur dan non rutin adalah ....",
                options: ["Sistem Digital", "Sistem Pembuat Keputusan", "Sistem Pendukung Keputusan", "Sistem Evaluasi Keputusan"],
                correct: "Sistem Pendukung Keputusan"
            },
            {
                question: "Proses bisnis dapat diperbaiki dan ditingkatkan dengan bantuan teknologi informasi melalui cara berikut ini, kecuali ....",
                options: ["otomatisasi proses bisnis", "efisiensi proses bisnis", "rekayasa ulang proses bisnis", "birokrasi proses bisnis"],
                correct: "birokrasi proses bisnis"
            },
            {
                question: "Beragam pandangan yang berbeda mengenai pendayagunaan sumber daya organisasi disebut ....",
                options: ["budaya organisasi", "politik organisasi", "struktur organisasi", "hirarkir organisasi"],
                correct: "politik organisasi"
            },
            {
                question: "Yang tidak termasuk faktor yang mempengaruhi interaksi teknologi informasi dengan organisasi adalah ....",
                options: ["keputusan manajemen operasional", "struktur organisasi", "operasional", "tak terduga"],
                correct: "keputusan manajemen operasional"
            },
            {
                question: "Keunikan barang digital dibandingkan dengan barang konvensional adalah ....",
                options: ["keputusan manajemen operasional", "struktur organisasi", "politik organisasi", "biaya produksi hanya sebesar biaya produksi unit pertama"],
                correct: "biaya produksi hanya sebesar biaya produksi unit pertama"
            },
            {
                question: "Pernyataan berikut yang tidak benar adalah ....",
                options: ["Teknologi informasi meminimalkan biaya", "Teknologi informasi meningkatkan efisiensi", "Teknologi informasi memperbesar nilai perusahaan", "Teknologi informasi mengurangi biaya transaksi"],
                correct: "Teknologi informasi mengurangi biaya transaksi"
            },
            {
                question: "Dalam strategi jaringan, nilai suatu perusahaan dan produknya akan naik jika ....",
                options: ["semakin banyak fiturnya", "semakin banyak penggunanya", "berkurang masalahnya", "berkurang kualitasnya"],
                correct: "semakin banyak penggunanya"
            },
            {
                question: "Yang tidak termasuk aktivitas pendukung dalam model rantai nilai bisnis adalah ....",
                options: ["manajemen", "administrasi", "pengadaan barang dan jasa", "layanan purna jual"],
                correct: "layanan purna jual"
            },
            {
                question: "Yang bukan termasuk strategi generik menghadapi persaingan menurut Porter adalah ....",
                options: ["biaya paling optimal", "biaya terendah", "diferensiasi produk", "fokus pada ceruk pasar"],
                correct: "biaya paling optimal"
            },
            {
                question: "Kemampuan memenangkan persaingan merupakan dampak dari adanya keunggulan ....",
                options: ["teknis", "bisnis", "kompetitif", "informasi"],
                correct: "kompetitif"
            },
            {
                question: "Gojek menawarkan layanan GoRide, GoFood, GoSend, dan GoPay dalam satu aplikasi adalah upaya untuk menang bersaing dengan cara ....",
                options: ["biaya terendah", "diferensiasi produk", "fokus pada ceruk pasar", "memperkuat hubungan dengan pemasok"],
                correct: "diferensiasi produk"
            },
            {
                question: "Penggunaan sensor dan telekomunikasi data pada barang disebut ....",
                options: ["internet 2.0", "Internet of Things", "internet Wireless", "Internet Superhighway"],
                correct: "Internet of Things"
            },
            {
                question: "Yang termasuk area abu-abu secara legal yang diakibatkan adanya sistem informasi baru adalah ...",
                options: ["sulitnya mengendalikan data", "belum diatur dengan undang-undang atau regulasi yang ada", "diimplementasikan secara sembrono", "tidak memperhatikan kepentingan pengguna tertentu"],
                correct: "belum diatur dengan undang-undang atau regulasi yang ada"
            },
            {
                question: "Pembajakan perangkat lunak masuk ke wilayah dimensi moral ....",
                options: ["hak dan kewajiban kepemilikan", "kualitas sistem", "kualitas hidup", "hak dan kewajiban informasi"],
                correct: "hak dan kewajiban kepemilikan"
            },
            {
                question: "Siap menanggung potensi kerugian atas keputusan yang dibuat disebut ....",
                options: ["liabilitas", "proses hukum", "akuntabilitas", "tanggung jawab"],
                correct: "akuntabilitas"
            },
            {
                question: "Mekanisme yang menentukan siapa yang bertindak dan siapa yang bertanggung jawab atas suatu tindakan disebut ....",
                options: ["liabilitas", "proses hukum", "akuntabilitas", "tanggung jawab"],
                correct: "akuntabilitas"
            },
            {
                question: "Aturan yang memungkinkan orang yang dirugikan oleh suatu tindakan (baik oleh individu, sistem, maupun organisasi) untuk mendapatkan kompensasi yang layak disebut .....",
                options: ["liabilitas", "proses hukum", "akuntabilitas", "tanggung jawab"],
                correct: "liabilitas"
            },
            {
                question: "Seseorang mencuri makanan dari supermarket karena keluarganya kelaparan, jika dievaluasi dengan Utilitarian Principle maka ....",
                options: ["dapat diterima karena pemilik supermarket kaya", "dapat diterima karena menyelamatkan keluarga dari kelaparan", "salah karena tidak ada orang yang mau dicuri barangnya", "salah karena mencuri itu salah untuk semua orang"],
                correct: "dapat diterima karena menyelamatkan keluarga dari kelaparan"
            },
            {
                question: "Edward Snowden membocorkan data bahwa pemerintah Amerika Serikat memata-matai warganya, menurut Golden Rule maka tindakan tersebut ....",
                options: ["dapat diterima untuk kepentingan publik", "salah karena melanggar hukum", "tidak dapat diterima, tidak ada yang mau dimata-matai", "netral"],
                correct: "tidak dapat diterima, tidak ada yang mau dimata-matai"
            },
            {
                question: "Mengedarkan lagu yang disalin dari komputer teman termasuk dalam dimensi moral ....",
                options: ["hak dan kewajiban kepemilikan", "kualitas sistem", "kualitas hidup", "hak dan kewajiban informasi"],
                correct: "hak dan kewajiban kepemilikan"
            },
            {
                question: "Seorang teknisi salah memasang perangkat yang membuat sistem perbankan macet dan merugikan nasabah termasuk dalam dimensi moral ....",
                options: ["hak dan kewajiban kepemilikan", "kualitas sistem", "kualitas hidup", "hak dan kewajiban informasi"],
                correct: "kualitas sistem"
            },
            {
                question: "Di negara Uni Eropa, pengguna dapat meminta Google menghapus catatan penggunaan miliknya, hal ini termasuk dalam dimensi moral ....",
                options: ["hak dan kewajiban kepemilikan", "kualitas sistem", "kualitas hidup", "hak dan kewajiban informasi"],
                correct: "hak dan kewajiban informasi"
            },
            {
                question: "Model penggunaan data pribadi di mana diasumsikan pemilik data mengijinkan kecuali dinyatakan secara eksplisit disebut ....",
                options: ["opt in", "opt out", "opt off", "Opt Send"],
                correct: "opt out"
            },
            {
                question: "Model penggunaan data pribadi di mana diasumsikan pemilik data tidak mengijinkan kecuali dinyatakan secara eksplisit disebut ....",
                options: ["Opt in", "opt out", "opt off", "opt send"],
                correct: "Opt in"
            },
            {
                question: "File kecil yang ditanamkan oleh suatu situs web ke perangkat milik pengunjungnya disebut ....",
                options: ["Bread crumb", "Biscuit", "Cookies", "Cookout"],
                correct: "Cookies"
            },
            {
                question: "Perlindungan terhadap buku pelajaran teknik sipil adalah ....",
                options: ["hak paten", "hak cipta", "hak milik", "hak guna"],
                correct: "hak cipta"
            },
            {
                question: "Perlindungan terhadap resep rahasia produk minuman adalah ....",
                options: ["merek dagang", "hak cipta", "hak paten", "rahasia dagang"],
                correct: "rahasia dagang"
            },
            {
                question: "Perlindungan terhadap teknologi komunikasi 4G/LTE adalah ....",
                options: ["merk dagang", "hak cipta", "hak paten", "rahasia dagang"],
                correct: "hak paten"
            },
            {
                question: "Yang bukan merupakan sumber energi baru terbarukan adalah Pembangkit listrik ....",
                options: ["tenaga surya", "tenaga gelombang", "tenaga uap", "tenaga angin"],
                correct: "tenaga uap"
            },
            {
                question: "Energi listrik pada pusat data milik perusahaan besar teknologi informasi dunia digunakan untuk mengoperasikan dan mendinginkan ....",
                options: ["generator", "perangkat komputer", "perangkat pembangkit daya", "perangkat lunak"],
                correct: "perangkat komputer"
            },
            {
                question: "Bahan beracun dan berbahaya di bawah ini yang tidak digunakan untuk membuat perangkat keras komputer adalah ....",
                options: ["cadmium", "Merkurium", "Arsenikum", "Radium"],
                correct: "Radium"
            },
            {
                question: "Menggunakan papan kunci dan tetikus secara terus-menerus berkontribusi pada kondisi yang disebut ....",
                options: ["Repetitive Sin Innocents", "Repetitive Stress Disorder", "Repetitive Post Traumatic", "Repetitive Stress Injury"],
                correct: "Repetitive Stress Injury"
            },
            {
                question: "SAN adalah ....",
                options: ["Storage Area Network", "Storage Attached Network", "Storage Array Network", "Storage Access Network"],
                correct: "Storage Area Network"
            },
            {
                question: "Antar muka yang menggunakan layar pada perangkat adalah ....",
                options: ["stylus", "Touch Screen", "Touch Pen", "digitizer"],
                correct: "Touch Screen"
            },
            {
                question: "Bahasa Pemrograman yang dapat dijalankan pada berbagai perangkat adalah ....",
                options: ["C#", "Assembler", "Pascal", "Java"],
                correct: "Java"
            },
            {
                question: "Ciri khas aplikasi dengan lisensi kode terbuka adalah ....",
                options: ["gratis dan boleh dijual", "gratis dan kode sumber disediakan", "berbayar dan terbatas", "berbayar dan boleh digandakan"],
                correct: "gratis dan kode sumber disediakan"
            },
            {
                question: "Menurut hukum Moore, kekuatan komputasi akan naik dua kali lipat setiap ....",
                options: ["18 bulan", "18 tahun", "18 minggu", "48 hari"],
                correct: "18 bulan"
            },
            {
                question: "Kelebihan komputer kuantum dibanding komputer biasa adalah dapat ....",
                options: ["bekerja sangat lama", "mengolah data 1 atau 0", "bekerja lebih sunyi", "mengolah data 1, 0, dan keduanya secara simultan"],
                correct: "mengolah data 1, 0, dan keduanya secara simultan"
            },
            {
                question: "Jenis komputer yang digunakan untuk menangani transaksi penting perbankan karena kehandalannya adalah ....",
                options: ["Blade Server", "Rack Server", "Mainframe", "Tablet"],
                correct: "Mainframe"
            },
            {
                question: "Aplikasi yang biasa digunakan untuk mengakses layanan komputasi awan adalah ....",
                options: ["Browser", "FTP client", "Word Processor", "Betrager"],
                correct: "Browser"
            },
            {
                question: "Kebijakan untuk memperbolehkan penggunaan perangkat pribadi untuk kepentingan kerja disebut ....",
                options: ["Byos", "BYOD", "Bson", "MyoB"],
                correct: "BYOD"
            },
            {
                question: "Sistem operasi perangkat bergerak yang dominan saat ini adalah ....",
                options: ["Android dan iOS", "Symbian dan Blackberry", "MS Windows CE dan Android", "iOS dan FreeBSD"],
                correct: "Android dan iOS"
            },
            {
                question: "Dalam model Packet Switching, data yang akan dikirim diperlakukan ....",
                options: ["dikirim langsung", "dijadikan beberapa paket data dan dikirim melalui jalur berbeda", "dijadikan beberapa paket data dan dikirim bergantian", "dijadikan beberapa paket data dan dikirim bersamaan"],
                correct: "dijadikan beberapa paket data dan dikirim melalui jalur berbeda"
            },
            {
                question: "Alat yang menghubungkan sebuah jaringan komputer dengan berbagai jaringan lain yang berbeda adalah ....",
                options: ["Hub", "Switch", "Repeater", "Router"],
                correct: "Router"
            },
            {
                question: "Kabel untuk menghubungkan jaringan telekomunikasi antar benua adalah ....",
                options: ["Fiber Glass", "Fiber Optic", "Fiber Soluble", "Fiber Kevlar"],
                correct: "Fiber Optic"
            },
            {
                question: "Alat telekomunikasi yang dapat menjangkau sepertiga permukaan bumi adalah ....",
                options: ["satelit", "WiFi", "BTS", "Bluetooth"],
                correct: "satelit"
            },
            {
                question: "Perangkat pengeras suara komputer tanpa kabel termasuk jaringan ....",
                options: ["WAN", "WLAN", "LAN", "PAN"],
                correct: "PAN"
            },
            {
                question: "Badan yang mengelola alokasi nama domain dan alamat IP adalah ....",
                options: ["ICANN", "WTO", "W3C", "IMF"],
                correct: "ICANN"
            },
            {
                question: "Alamat IP yang terdiri atas 4 blok angka antara 0-255 adalah versi ....",
                options: ["IP v1", "IP v2", "IP v4", "IP v6"],
                correct: "IP v4"
            },
            {
                question: "Energi listrik pada pusat data milik perusahaan besar teknologi informasi dunia digunakan untuk mengoperasikan dan mendinginkan ....",
                options: ["generator", "perangkat komputer", "perangkat pembangkit daya", "perangkat lunak"],
                correct: "perangkat komputer"
            },
            {
                question: "Layanan telepon menggunakan jalur Internet adalah ....",
                options: ["VoIP", "VoLTE", "VoTTA", "MIRC"],
                correct: "VoIP"
            },
            {
                question: "Server Internet yang melayani permintaan dokumen dari klien adalah ....",
                options: ["Web Server", "File Server", "Application Server", "Database Server"],
                correct: "Web Server"
            },
            {
                question: "Malware yang membajak komputer korban dan menuntut tebusan untuk melepaskannya adalah ....",
                options: ["virus", "worms", "Adware", "Ransomware"],
                correct: "Ransomware"
            },
            {
                question: "Upaya melumpuhkan sistem kelistrikan suatu negara oleh aparat negara lain disebut ....",
                options: ["peperangan siber", "terorisme siber", "sibernetika", "kejahatan komputer"],
                correct: "peperangan siber"
            },
            {
                question: "Program khusus yang secara mandiri menggandakan dirinya sendiri dari satu komputer ke komputer lain melalui jaringan komputer disebut ....",
                options: ["virus", "Worms", "Adware", "Ransomware"],
                correct: "Worms"
            },
            {
                question: "Kerapuhan perangkat lunak yang belum diketahui oleh yang berkepentingan (pembuat dan pengguna) sehingga tidak dilakukan tindakan mitigasi disebut ....",
                options: ["Bugs", "Error", "Zero Day Vulnerabilities", "Inherent Vulnerabilities"],
                correct: "Zero Day Vulnerabilities"
            },
            {
                question: "Malware yang dirancang untuk menyerang komputer pengendali mesin industri adalah ....",
                options: ["Stoned", "Wanna Cry", "Stuxnet", "Petya"],
                correct: "Stuxnet"
            },
            {
                question: "Kejahatan dengan menggunakan akses poin wifi palsu yang seolah-olah sebagai penyedia layanan akses wifi yang terpercaya untuk mencuri data disebut ....",
                options: ["Evil Twins", "Wanna Cry", "Stuxnet", "Petya"],
                correct: "Evil Twins"
            },
            {
                question: "Wifi dianggap kurang aman, karena ....",
                options: ["mudah dipakai", "sering crash", "mudah disadap", "lambat"],
                correct: "mudah disadap"
            },
            {
                question: "Pembaharuan perangkat lunak untuk menutup celah keamanan disebut sebagai ....",
                options: ["paten", "Compiler", "Interpreter", "Patch"],
                correct: "Patch"
            },
            {
                question: "Bujukan dan tipu daya kepada seseorang untuk memberikan akun dan password disebut sebagai ....",
                options: ["Evil Twins", "Social Network", "Stuxnet", "Social Engineering"],
                correct: "Social Engineering"
            },
            {
                question: "Membanjiri server yang dituju dengan permintaan atas data yang berlebihan sehingga diharapkan server yang dituju kewalahan dan berhenti bekerja disebut sebagai ....",
                options: ["MsDOS", "PC-DOS", "DoS", "Orbos"],
                correct: "DoS"
            },
            {
                question: "Kerahasiaan rekam medis pasien dilindungi oleh regulasi ....",
                options: ["Peraturan Menteri Kesehatan Nomor 269 Tahun 2008", "Peraturan Menteri PAN RB Nomor 269 Tahun 2008", "UU Nomor 5 Tahun 2011", "UU Nomor 19 Tahun 2006"],
                correct: "Peraturan Menteri Kesehatan Nomor 269 Tahun 2008"
            },
            {
                question: "Menggunakan PIN dan Kartu ATM untuk bertransaksi melalui mesin ATM adalah upaya ....",
                options: ["manajemen risiko", "manajemen identitas", "manajemen laba", "manajemen sumber daya"],
                correct: "manajemen identitas"
            },
            {
                question: "Membeli asuransi untuk gedung pusat data termasuk upaya ....",
                options: ["manajemen risiko", "manajemen identitas", "manajemen laba", "manajemen sumber daya"],
                correct: "manajemen risiko"
            },
            {
                question: "Profesi Computer Forensics bertanggung jawab untuk ....",
                options: ["merekayasa data", "memanipulasi gambar", "menyajikan bukti ke pengadilan", "menangkap pelaku kejahatan komputer"],
                correct: "menyajikan bukti ke pengadilan"
            },
            {
                question: "Konfirmasi rekening tujuan dan jumlah sebelum melakukan transfer dana di ATM merupakan bagian dari ....",
                options: ["pengendalian keluaran", "pengendalian masukan", "pengendalian proses", "pengendalian data"],
                correct: "pengendalian masukan"
            },
            {
                question: "PIN kartu ATM diberikan kepada nasabah menggunakan amplop tertutup dan tersegel adalah upaya dari ....",
                options: ["pengendalian keluaran", "pengendalian masukan", "pengendalian proses", "pengendalian data"],
                correct: "pengendalian masukan"
            },
            {
                question: "Pintu ruang komputer dikunci dan hanya orang tertentu yang boleh membawa kuncinya adalah contoh dari ....",
                options: ["pengendalian keluaran", "pengendalian masukan", "pengendalian Umum", "pengendalian aplikasi"],
                correct: "pengendalian Umum"
            },
            {
                question: "Menggunakan genset dan baterai cadangan merupakan upaya ....",
                options: ["disaster preparedness", "disaster mitigation", "disaster recovery plan", "disaster crisis"],
                correct: "disaster preparedness"
            },
            {
                question: "Kantor cabang bank di Solo mengambil alih pelayanan nasabah ketika kantor cabang di Yogya terkena bencana merupakan bagian dari ....",
                options: ["disaster preparedness", "disaster mitigation", "disaster recovery plan", "business continuity planning"],
                correct: "business continuity planning"
            },
            {
                question: "Tujuan audit sistem informasi adalah ...",
                options: ["menguji keamanan sistem informasi", "memeriksa apakah kebijakan keamanan dipatuhi", "menemukan kesalahan personel sistem informasi", "menguji kesiapan sistem informasi menghadapi bencana"],
                correct: "memeriksa apakah kebijakan keamanan dipatuhi"
            },
            {
                question: "Kumpulan bit disebut ....",
                options: ["Byte", "Binary digit", "Bite", "Bittermen"],
                correct: "Byte"
            },
            {
                question: "Data yang sama disimpan di beberapa tempat disebut sebagai ....",
                options: ["Recycle", "Redundancy", "Reuse", "Register"],
                correct: "Redundancy"
            },
            {
                question: "Sesuatu yang datanya akan direkam dan disimpan oleh suatu organisasi disebut ....",
                options: ["Ekuitas", "Aset", "Equilibrium", "Entitas"],
                correct: "Entitas"
            },
            {
                question: "Karakteristik entitas disebut sebagai ....",
                options: ["Atribut", "Aset", "Ekuitas", "Entitas"],
                correct: "Atribut"
            },
            {
                question: "Perangkat lunak untuk mengelola data secara terpusat adalah ....",
                options: ["DBMS", "NTFS", "APRS", "SPSS"],
                correct: "DBMS"
            },
            {
                question: "Model basis data yang menggambarkan data sebagai tabel dua dimensi adalah ....",
                options: ["Relativitas", "Assymetry", "Relasional", "Algoritma"],
                correct: "Relasional"
            },
            {
                question: "Bahasa standar untuk memanipulasi dan mengelola basis data adalah ....",
                options: ["SQL", "Python", "C#", "Visual Basic"],
                correct: "SQL"
            },
            {
                question: "Proses untuk menormalkan suatu relasi dalam basis data dengan memecah satu tabel menjadi beberapa tabel disebut ....",
                options: ["Optimasi", "Normalisasi", "Denormalisasi", "Defragmentasi"],
                correct: "Normalisasi"
            },
            {
                question: "Basis data khusus untuk mengelola Big Data adalah ....",
                options: ["MySQL", "MongoDB", "PostgreSQL", "Transact-SQL"],
                correct: "MongoDB"
            },
            {
                question: "Proses memasukkan data dari sistem pengolahan transaksi ke Data Warehouse adalah ....",
                options: ["ETL", "ECR", "ECM", "ERP"],
                correct: "ETL"
            },
            {
                question: "Agar dapat digunakan secara optimal pengetahuan membutuhkan ....",
                options: ["kompetisi", "koperasi", "kooptasi", "kolaborasi"],
                correct: "kolaborasi"
            },
            {
                question: "Keterampilan untuk mengukir kayu termasuk pengetahuan ....",
                options: ["tacit", "eksplisit", "terstruktur", "tidak terstruktur"],
                correct: "tacit"
            },
            {
                question: "Kebijakan tertulis mengenai penggunaan laboratorium sebuah universitas merupakan pengetahuan ....",
                options: ["tacit", "eksplisit", "terstruktur", "tidak terstruktur"],
                correct: "eksplisit"
            },
            {
                question: "Skema untuk membuat klasifikasi pengetahuan disebut ....",
                options: ["Taksasi", "Taksidermi", "Taksonomi", "Taksaka"],
                correct: "Taksonomi"
            },
            {
                question: "Aplikasi yang banyak digunakan untuk pembelajaran jarak jauh adalah ....",
                options: ["TLS", "LMS", "IMS", "TEB"],
                correct: "LMS"
            },
            {
                question: "Arsitek rumah biasanya menggunakan aplikasi ....",
                options: ["CAD", "CAM", "VR", "Pokemon Go"],
                correct: "CAD"
            },
            {
                question: "Alat simulasi untuk ujian Surat Izin Mengemudi merupakan contoh dari ....",
                options: ["CAD", "CAM", "VR", "Pokemon Go"],
                correct: "VR"
            },
            {
                question: "MIT OpenCourseWare menggunakan aplikasi ....",
                options: ["TLS", "LMS", "IMS", "TEB"],
                correct: "LMS"
            },
            {
                question: "Manusia membutuhkan bantuan kecerdasan buatan dalam manajemen pengetahuan ....",
                options: ["Setiap saat", "Tidak pernah", "Batasnya tidak ada", "Jumlah data dan informasi sangat besar"],
                correct: "Jumlah data dan informasi sangat besar"
            },
            {
                question: "Pembelajaran organisasi mayoritas melibatkan pengetahuan yang bersifat ....",
                options: ["tacit", "eksplisit", "terstruktur", "tidak terstruktur"],
                correct: "tacit"
            },
            {
                question: "Perusahaan besar dengan banyak divisi, usaha berskala besar, dan anak perusahaan disebut ....",
                options: ["Entrepreneur", "Socialpreneur", "Enterprise", "Technopreneur"],
                correct: "Enterprise"
            },
            {
                question: "Dampak dari pembentukan divisi yang saling berdiri sendiri dalam suatu perusahaan besar adalah ....",
                options: ["silo informasi", "kuasi informasi", "politik organisasi", "isolasi informasi"],
                correct: "silo informasi"
            },
            {
                question: "Proses pengiriman barang merupakan bagian dari modul ERP ....",
                options: ["akuntansi dan keuangan", "manufaktur dan operasi", "penjualan dan pemasaran", "sumber daya manusia"],
                correct: "manufaktur dan operasi"
            },
            {
                question: "Pengajuan izin cuti pegawai merupakan bagian dari modul ERP ....",
                options: ["akuntansi dan keuangan", "manufaktur dan operasi", "penjualan dan pemasaran", "sumber daya manusia"],
                correct: "sumber daya manusia"
            },
            {
                question: "Petani tembakau bagi perusahaan rokok merupakan bagian segmen rantai pasokan ....",
                options: ["Streamer", "Upstream", "Internal", "Downstream"],
                correct: "Upstream"
            },
            {
                question: "Minimarket merupakan bagian rantai pasokan yang masuk dalam segmen ....",
                options: ["Streamer", "Upstream", "Internal", "Downstream"],
                correct: "Downstream"
            },
            {
                question: "Kegiatan produksi yang dipicu oleh estimasi penjualan disebut ....",
                options: ["push manufacturing", "pull manufacturing", "modern manufacturing", "traditional manufacturing"],
                correct: "push manufacturing"
            },
            {
                question: "Modul yang membantu tenaga penjualan dalam perangkat lunak CRM adalah ....",
                options: ["SFA", "POS", "AR", "AP"],
                correct: "SFA"
            },
            {
                question: "Bagian CRM yang menentukan apa saja barang yang paling diminati pembeli usia muda adalah ....",
                options: ["operasional", "finansial", "analitis", "sekuensial"],
                correct: "analitis"
            },
            {
                question: "Petugas Call Centre menggunakan bagian CRM ....",
                options: ["Operasional", "Finansial", "Analitis", "Sekuensial"],
                correct: "Operasional"
            },
            {
                question: "Model bisnis untuk toko online seperti Blibli.com adalah ....",
                options: ["pengepul", "pengecer", "perantara", "media sosial"],
                correct: "pengecer"
            },
            {
                question: "Tokopedia termasuk perusahaan dengan model bisnis ....",
                options: ["pengepul", "pengecer", "perantara", "media sosial"],
                correct: "perantara"
            },
            {
                question: "Pembelian karet alam bagi perusahaan ban termasuk model perdagangan ....",
                options: ["C2C", "G2G", "B2C", "B2B"],
                correct: "B2B"
            },
            {
                question: "Amazon termasuk model perdagangan ....",
                options: ["C2C", "G2G", "B2C", "B2B"],
                correct: "B2C"
            },
            {
                question: "Pendapatan Google terbesar berasal dari ....",
                options: ["penjualan smartphone Pixel", "penjualan Google Drive", "iklan", "penjualan Android"],
                correct: "iklan"
            },
            {
                question: "Model pendapatan Joox adalah ....",
                options: ["premium", "freemium", "berlangganan", "iklan"],
                correct: "freemium"
            },
            {
                question: "Traveloka, AirBnB, Tiket.com adalah contoh perusahaan yang menggunakan model bisnis ....",
                options: ["penyedia konten", "pedagang eceran", "penjual iklan", "perantara transaksi"],
                correct: "perantara transaksi"
            },
            {
                question: "Youtube adalah contoh perusahaan yang menggunakan model bisnis ....",
                options: ["penyedia konten", "pedagang eceran", "penjual iklan", "perantara transaksi"],
                correct: "penyedia konten"
            },
            {
                question: "Ruang Guru adalah contoh perusahaan yang menggunakan model bisnis ....",
                options: ["penyedia konten", "pedagang eceran", "penjual iklan", "perantara transaksi"],
                correct: "penyedia konten"
            },
            {
                question: "Netflix mampu bersaing dengan Blockbuster karena meniadakan biaya sewa ....",
                options: ["kios", "komputer", "tahan", "rumah"],
                correct: "tahan"
            },
            {
                question: "Menghitung gaji bulanan karyawan termasuk jenis keputusan ....",
                options: ["rasional", "terstruktur", "semi terstruktur", "tidak terstruktur"],
                correct: "terstruktur"
            },
            {
                question: "Memilih pemasok untuk barang tertentu termasuk jenis keputusan ....",
                options: ["rasional", "terstruktur", "semi terstruktur", "tidak terstruktur"],
                correct: "semi terstruktur"
            },
            {
                question: "Membuat produk baru termasuk jenis keputusan ....",
                options: ["rasional", "terstruktur", "semi terstruktur", "tidak terstruktur"],
                correct: "tidak terstruktur"
            },
            {
                question: "Tiga kategori peran manajerial menurut Mintzberg adalah ....",
                options: ["interpersonal, informational, keputusan", "pengendalian, kepemimpinan, pengawasan", "operasional, manajerial, eksekutif", "budaya, organisasional, teknis"],
                correct: "interpersonal, informational, keputusan"
            },
            {
                question: "Menolak kebenaran informasi karena konsepsi yang dimiliki disebut ....",
                options: ["filter redaksional", "filter reduksional", "filter abrasif", "filter manajerial"],
                correct: "filter manajerial"
            },
            {
                question: "Konsistensi struktur data merupakan dimensi kualitas data ....",
                options: ["integritas", "akurasi", "ketepatan waktu", "kelengkapan"],
                correct: "integritas"
            },
            {
                question: "Membuat anggaran merupakan perwujudan fungsi manajemen ....",
                options: ["perencanaan", "pengendalian", "koordinasi", "pengawasan"],
                correct: "perencanaan"
            },
            {
                question: "Memberikan surat peringatan pada karyawan yang melanggar aturan merupakan perwujudan fungsi manajemen ....",
                options: ["perencanaan", "pengendalian", "koordinasi", "pengawasan"],
                correct: "pengendalian"
            },
            {
                question: "Membaca dan mempelajari laporan penjualan harian merupakan perwujudan fungsi manajemen ....",
                options: ["perencanaan", "pengendalian", "koordinasi", "pengawasan"],
                correct: "pengawasan"
            },
            {
                question: "Mengajak diskusi karyawan yang mengalami penurunan kinerja untuk mencari tahu penyebabnya merupakan tahapan pembuatan keputusan ....",
                options: ["pencarian fakta", "perancangan solusi", "pemilihan alternatif solusi", "penerapan solusi"],
                correct: "pemilihan alternatif solusi"
            },
            {
                question: "Analisis prediktif dapat digunakan untuk hal berikut, kecuali ....",
                options: ["mengantisipasi tanggapan pada produk baru", "mengidentifikasi produk yang paling menguntungkan", "menentukan rute pengiriman barang terbaik", "menilai kelayakan kredit nasabah"],
                correct: "menilai kelayakan kredit nasabah"
            },
            {
                question: "Dalam BSC, kinerja diukur berdasarkan ....",
                options: ["KPI", "PIR", "WRAP", "Perspektif (Keuangan, Pelanggan, Proses Bisnis Internal, Pembelajaran & Pertumbuhan)"],
                correct: "Perspektif (Keuangan, Pelanggan, Proses Bisnis Internal, Pembelajaran & Pertumbuhan)"
            },
            {
                question: "Analisa sensitivitas banyak digunakan dalam sistem ....",
                options: ["DSS", "DSS", "OLAP", "NDA"],
                correct: "DSS"
            },
            {
                question: "Media untuk menampilkan kinerja perusahaan berdasarkan kriteria tertentu adalah ....",
                options: ["Bashcam", "Scoring", "Dashboard", "KPI"],
                correct: "Dashboard"
            },
            {
                question: "Yang tidak termasuk alat dalam analisis prediktif adalah ....",
                options: ["Statistik", "Ekonometri", "Data mining", "Intuisi"],
                correct: "Intuisi"
            },
            {
                question: "Fasilitas untuk menelusuri data yang menjadi dasar suatu laporan disebut ....",
                options: ["drill down", "throughput", "drilling", "data staging"],
                correct: "drill down"
            },
            {
                question: "Menurunnya keterlambatan pengiriman barang merupakan KPI untuk Scorecard dalam dimensi ....",
                options: ["Keuangan", "Pembelajaran dan pertumbuhan", "Proses Bisnis Internal", "Pelanggan"],
                correct: "Proses Bisnis Internal"
            },
            {
                question: "Naiknya kas masuk merupakan KPI untuk Scorecard dalam dimensi ....",
                options: ["Keuangan", "Pembelajaran dan pertumbuhan", "Proses Bisnis Internal", "Pelanggan"],
                correct: "Keuangan"
            },
            {
                question: "Menurunnya piutang tidak tertagih merupakan KPI untuk Scorecard dalam dimensi ....",
                options: ["Keuangan", "Pembelajaran dan pertumbuhan", "Proses Bisnis Internal", "Pelanggan"],
                correct: "Keuangan"
            },
            {
                question: "Model yang dominan digunakan dalam DSS adalah ....",
                options: ["ikonik", "mental", "analog", "matematis"],
                correct: "matematis"
            },
            {
                question: "SDLC digunakan secara resmi sejak ....",
                options: ["1960-an", "1970-an", "2010-an", "1980-an"],
                correct: "1960-an"
            },
            {
                question: "Komputerisasi proses penggajian merupakan contoh ....",
                options: ["otomatisasi proses bisnis", "rasionalisasi proses bisnis", "perancangan ulang proses bisnis", "pergeseran paradigma"],
                correct: "otomatisasi proses bisnis"
            },
            {
                question: "Gojek merupakan contoh dari ....",
                options: ["otomatisasi proses bisnis", "rasionalisasi proses bisnis", "perancangan ulang proses bisnis", "pergeseran paradigma"],
                correct: "pergeseran paradigma"
            },
            {
                question: "Pengembangan sistem pada masa tutup pembukuan tidak layak secara ....",
                options: ["teknis", "hukum", "ekonomis", "jadwal"],
                correct: "jadwal"
            },
            {
                question: "Jika suatu sistem informasi di perusahaan eceran membutuhkan komputer super, maka tidak layak secara ....",
                options: ["teknis", "hukum", "ekonomis", "jadwal"],
                correct: "teknis"
            },
            {
                question: "Program penghitung pajak salah menerapkan tarif PPh Pasal 25 berarti tidak layak secara ...",
                options: ["teknis", "hukum", "ekonomis", "jadwal"],
                correct: "hukum"
            },
            {
                question: "Pengembangan sistem informasi yang mahal dan lebih mahal daripada manfaatnya tidak layak secara ....",
                options: ["teknis", "hukum", "ekonomis", "jadwal"],
                correct: "ekonomis"
            },
            {
                question: "Pemangku kepentingan mana yang sebaiknya diikutsertakan dalam pengembangan sistem informasi ....",
                options: ["pemerintah", "konsumen", "pengguna", "pemegang saham"],
                correct: "pengguna"
            },
            {
                question: "Pemangku kepentingan yang terkait dengan kelayakan secara hukum ....",
                options: ["pemerintah", "konsumen", "pengguna", "pemegang saham"],
                correct: "pemerintah"
            },
            {
                question: "Alat bantu aplikasi komputer untuk mengembangkan sistem informasi ....",
                options: ["CASE", "CAST", "CEASE", "CARO"],
                correct: "CASE"
            },
            {
                question: "Ukuran kesuksesan proyek adalah ....",
                options: ["tepat waktu dan anggaran", "anggaran dihabiskan", "selesai lebih cepat", "laporan lengkap"],
                correct: "tepat waktu dan anggaran"
            },
            {
                question: "Yang bukan variabel utama keberhasilan proyek adalah ....",
                options: ["pemasok", "risiko", "waktu", "kualitas"],
                correct: "pemasok"
            },
            {
                question: "Keamanan sistem informasi masuk dalam kategori ....",
                options: ["must have", "should have", "could have", "will not have"],
                correct: "must have"
            },
            {
                question: "Bagi perusahaan jasa, sistem informasi persediaan dagangan termasuk kategori ....",
                options: ["must have", "should have", "could have", "will not have"],
                correct: "should have"
            },
            {
                question: "Bagi perusahaan dagang, sistem informasi persediaan dagangan termasuk kategori ....",
                options: ["must have", "should have", "could have", "will not have"],
                correct: "must have"
            },
            {
                question: "Bagi perusahaan konsultan manajemen, sistem informasi pengadaan barang termasuk kategori ....",
                options: ["must have", "should have", "could have", "will not have"],
                correct: "should have"
            },
            {
                question: "Yang menunjukkan rencana dan realisasi proyek ....",
                options: ["CPM", "PERT", "Gantt Chart", "Chart of Account"],
                correct: "Gantt Chart"
            },
            {
                question: "Yang tidak menunjukkan titik kritis suatu proyek ....",
                options: ["CPM", "PERT", "Gantt Chart", "Chart of Account"],
                correct: "Gantt Chart"
            },
            {
                question: "Ukuran proyek dinilai dengan ....",
                options: ["estimasi", "prediksi", "biaya dan waktu pengerjaan", "intuisi"],
                correct: "biaya dan waktu pengerjaan"
            },
            {
                question: "Potensi munculnya masalah yang mengganggu penyelesaian proyek adalah ....",
                options: ["risiko", "biaya", "waktu", "tenaga"],
                correct: "risiko"
            }
        ];

        let selectedQuestions = [];
        const numberOfQuestions = 50;

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        function generateQuiz() {
            shuffleArray(allQuestions);
            selectedQuestions = allQuestions.slice(0, numberOfQuestions);

            const quizForm = document.getElementById('quizForm');
            quizForm.innerHTML = ''; // Clear previous questions

            selectedQuestions.forEach((q, index) => {
                const questionSection = document.createElement('div');
                questionSection.classList.add('question-section');

                const questionText = document.createElement('p');
                questionText.classList.add('question-text');
                questionText.textContent = `${index + 1}. ${q.question}`;
                questionSection.appendChild(questionText);

                const optionsContainer = document.createElement('div');
                optionsContainer.classList.add('options-container');

                shuffleArray(q.options); // Shuffle options for each question

                q.options.forEach(option => {
                    const label = document.createElement('label');
                    const input = document.createElement('input');
                    input.type = 'radio';
                    input.name = `question${index}`;
                    input.value = option;
                    label.appendChild(input);
                    label.appendChild(document.createTextNode(option));
                    optionsContainer.appendChild(label);
                });
                questionSection.appendChild(optionsContainer);
                quizForm.appendChild(questionSection);
            });

            document.getElementById('results').style.display = 'none';
            document.querySelector('.submit-btn').style.display = 'block';
        }

        function submitQuiz() {
            let score = 0;
            const quizForm = document.getElementById('quizForm');
            const questionSections = quizForm.querySelectorAll('.question-section');

            questionSections.forEach((section, index) => {
                const question = selectedQuestions[index];
                const selectedOption = quizForm.querySelector(`input[name="question${index}"]:checked`);
                const allLabels = section.querySelectorAll('label');

                // Reset previous feedback styles
                allLabels.forEach(label => {
                    label.classList.remove('correct-answer', 'incorrect-answer');
                });
                section.classList.remove('correct', 'incorrect');

                if (selectedOption) {
                    if (selectedOption.value === question.correct) {
                        score++;
                        selectedOption.parentElement.classList.add('correct-answer');
                        section.classList.add('correct');
                    } else {
                        selectedOption.parentElement.classList.add('incorrect-answer');
                        section.classList.add('incorrect');
                        // Highlight the correct answer
                        allLabels.forEach(label => {
                            if (label.textContent.trim() === question.correct) {
                                label.classList.add('correct-answer');
                            }
                        });
                    }
                } else {
                    // If no option is selected, still show the correct answer
                    section.classList.add('incorrect'); // Mark as incorrect if not answered
                    allLabels.forEach(label => {
                        if (label.textContent.trim() === question.correct) {
                            label.classList.add('correct-answer');
                        }
                    });
                }

                // Disable all radios after submission
                section.querySelectorAll('input[type="radio"]').forEach(radio => radio.disabled = true);
            });

            document.getElementById('score').textContent = score;
            document.getElementById('results').style.display = 'block';
            document.querySelector('.submit-btn').style.display = 'none';
        }

        function resetQuiz() {
            generateQuiz(); // Regenerate quiz with new random questions
        }

        // Initialize quiz on page load
        document.addEventListener('DOMContentLoaded', generateQuiz);
    </script>
</body>
</html>
