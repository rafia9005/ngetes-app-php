## layanan nikah
```php
<?php
// Include file konfigurasi
include '../../config/config.php';

// Memeriksa apakah form telah di-submit
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  // Mendapatkan nilai dari form
  $akte_kelahiran = $_FILES["akte_kelahiran"]["name"];
  $surat_baptis = $_FILES["surat_baptis"]["name"];
  $surat_pemberkatan_perkawinan = $_FILES["surat_pemberkatan_perkawinan"]["name"];
  $surat_keterangan_sehat = $_FILES["surat_keterangan_sehat"]["name"];
  $ktp = $_FILES["ktp"]["name"];
  $nomer = $_POST['nomer'];

  // Memindahkan file yang di-upload ke folder yang diinginkan
  $targetDir = "uploads/nikah/";
  move_uploaded_file($_FILES["akte_kelahiran"]["tmp_name"], $targetDir . basename($akte_kelahiran));
  move_uploaded_file($_FILES["surat_baptis"]["tmp_name"], $targetDir . basename($surat_baptis));
  move_uploaded_file($_FILES["surat_pemberkatan_perkawinan"]["tmp_name"], $targetDir . basename($surat_pemberkatan_perkawinan));
  move_uploaded_file($_FILES["surat_keterangan_sehat"]["tmp_name"], $targetDir . basename($surat_keterangan_sehat));
  move_uploaded_file($_FILES["ktp"]["tmp_name"], $targetDir . basename($ktp));

  // Menghubungkan ke database
  include '../../config/config.php';

  // Menyimpan data ke database
  $sql = "INSERT INTO keterangan_nikah (akte_kelahiran, surat_baptis, surat_pemberkatan_perkawinan, surat_keterangan_sehat, ktp, nomer)
          VALUES ('$akte_kelahiran', '$surat_baptis', '$surat_pemberkatan_perkawinan', '$surat_keterangan_sehat', '$ktp', '$nomer')";
  if (mysqli_query($conn, $sql)) {
    echo "Data berhasil di-upload ke database.";
  } else {
    echo "Error: " . $sql . "<br>" . mysqli_error($conn);
  }

  // Menutup koneksi database
  mysqli_close($conn);
}
?>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
<script>
    var url = "../index.php"; // url tujuan
    var count = 1; // dalam detik
    function countDown() {
        if (count > 0) {
            count--;
            var waktu = count + 1;
            $('#kata').html('<b>Halaman Ini Akan Otomatis Di Redirect KE </b> ' + url + ' dalam ' + waktu + ' detik.');
            setTimeout("countDown()", 0);   
        } else {
            window.location.href = url;
        }
    }
    countDown();
</script>
```

```php
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="shortcut icon" href="assets/images/favicon.svg" type="image/x-icon" />
    <title>
        <?php if (!$is_admin): ?>
            Layanan Kependudukan
        <?php endif; ?>
        <?php if ($user['role'] === 'admin'): ?>
            Data Kependudukan
        <?php endif; ?>
    </title>

    <!-- ========== All CSS files linkup ========= -->
    <link rel="stylesheet" href="../assets/css/bootstrap.min.css" />
    <link rel="stylesheet" href="../assets/css/lineicons.css" />
    <link rel="stylesheet" href="../assets/css/materialdesignicons.min.css" />
    <link rel="stylesheet" href="../assets/css/fullcalendar.css" />
    <link rel="stylesheet" href="../assets/css/main.css" />
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
        integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw=="
        crossorigin="anonymous" referrerpolicy="no-referrer" />
</head>

<body>
    <!-- ======== sidebar-nav start =========== -->
    <aside class="sidebar-nav-wrapper">
        <div class="navbar-logo">
            <a href="index.html">
                <img src="../assets/image/logo.png" alt="logo" width="70px" />
            </a>
        </div>
        <nav class="sidebar-nav">
            <ul>
                <li class="nav-item nav-item-has-childre">
                    <a href="index.php" aria-expanded="false" aria-label="Toggle navigation">
                        <span class="icon">
                            <i class="fa-solid fa-list"></i>
                        </span>
                        <span class="text">
                            <?php if (!$is_admin): ?>
                                Layanan Umum
                            <?php endif; ?>
                            <?php if ($user['role'] === 'admin'): ?>
                                Data Umum
                            <?php endif; ?>
                        </span>
                    </a>
                </li>
                <li class="nav-item nav-item-has-childre">
                    <a href="LayananKependudukan.php" aria-expanded="false" aria-label="Toggle navigation">
                        <span class="icon">
                            <i class="fa-solid fa-layer-group"></i>
                        </span>
                        <span class="text">
                            <?php if (!$is_admin): ?>
                                Layanan Kependudukan
                            <?php endif; ?>
                            <?php if ($user['role'] === 'admin'): ?>
                                Data Kependudukan
                            <?php endif; ?>
                        </span>
                    </a>
                </li>
                <li class="nav-item nav-item-has-children">
                    <a href="LayananNikah.php" aria-expanded="false" aria-label="Toggle navigation">
                        <span class="icon">
                            <i class="fa-solid fa-wand-magic-sparkles"></i>
                        </span>
                        <span class="text">
                            <?php if (!$is_admin): ?>
                                Layanan Nikah
                            <?php endif; ?>
                            <?php if ($user['role'] === 'admin'): ?>
                                Data Nikah
                            <?php endif; ?>
                        </span>
                    </a>
                </li>
            </ul>
        </nav>
        <div class="promo-box">
            <a href="logout.php" rel="nofollow" class="main-btn primary-btn btn-hover">
                Log Out
            </a>
        </div>
    </aside>
    <div class="overlay"></div>
    <!-- ======== sidebar-nav end =========== -->

    <!-- ======== main-wrapper start =========== -->
    <main class="main-wrapper">
        <!-- ========== header start ========== -->
        <header class="header">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-lg-5 col-md-5 col-6">
                        <div class="header-left d-flex align-items-center">
                            <div class="menu-toggle-btn mr-20">
                                <button id="menu-toggle" class="main-btn primary-btn btn-hover">
                                    <i class="lni lni-chevron-left me-2"></i> Menu
                                </button>
                            </div>
                            <div class="header-search d-none d-md-flex">
                                <form action="#">
                                    <input type="text" placeholder="Search..." />
                                    <button><i class="lni lni-search-alt"></i></button>
                                </form>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-7 col-md-7 col-6">
                        <div class="header-right">
                            <div class="filter-box ml-15 d-none d-md-flex">
                                <button class="" type="button" id="filter">
                                    <img src="../assets/image/logo.png" alt="" width="30px">
                                </button>
                            </div>
                            <!-- filter end -->
                            <!-- profile start -->
                            <div class="profile-box ml-15">
                                <button class="dropdown-toggle bg-transparent border-0" type="button" id="profile"
                                    data-bs-toggle="dropdown" aria-expanded="false">
                                    <div class="profile-info">
                                        <div class="info">
                                            <h6>
                                                <?= $user['username'] ?>
                                            </h6>
                                        </div>
                                    </div>
                                    <i class="lni lni-chevron-down"></i>
                                </button>
                            </div>
                            <!-- profile end -->
                        </div>
                    </div>
                </div>
            </div>
        </header>
        <!-- ========== header end ========== -->

        <!-- ========== section start ========== -->
        <section class="section">
            <div class="container-fluid">
                <!-- ========== title-wrapper start ========== -->
                <div class="title-wrapper pt-30">
                    <div class="row align-items-center">
                        <div class="col-md-6">
                            <div class="titlemb-30">
                                <h2>Layanan Kependudukan</h2>
                            </div>
                        </div>
                        <!-- end col -->
                        <div class="col-md-6">
                            <div class="breadcrumb-wrapper mb-30">
                                <nav aria-label="breadcrumb">
                                    <ol class="breadcrumb">
                                        <li class="breadcrumb-item">
                                            <a href="#0">Dashboard</a>
                                        </li>
                                        <li class="breadcrumb-item active" aria-current="page">
                                            Kependudukan
                                        </li>
                                    </ol>
                                </nav>
                            </div>
                        </div>
                        <!-- end col -->
                    </div>
                    <!-- end row -->
                </div>
                <!-- === menu === -->


                <!-- tampilan admin -->
                <?php if ($user['role'] === 'admin'): ?>
                    <div class="card-style mb-30">
                        <p>Data Keterangan Pindah</p>
                        <div class="table-wrapper table-responsive" style="max-height: 360px; overflow-y: scroll;">
                            <?php
$query = "SELECT * FROM keterangan_nikah";
$result = mysqli_query($conn, $query);

// Mengecek apakah query berhasil dieksekusi
if ($result) {
    // Mengecek apakah ada data yang dihasilkan
    if (mysqli_num_rows($result) > 0) {
        // Menampilkan tabel
        echo "<table class='table striped-table'>";
        echo "<tr>";
        echo "<th class='p-2'>Foto Copy Akte Kelahiran</th>";
        echo "<th class='p-2'>Foto Copy Surat Baptis</th>";
        echo "<th class='p-2'>Foto Copy Surat Pemberkatan</th>";
        echo "<th class='p-2'>Surat Keterangan Sehat</th>";
        echo "<th class='p-2'>Foto Copy KTP</th>";
        echo "<th class='p-2'>Chat Wa</th>";
        echo "</tr>";

        // Menampilkan data dalam tabel
        while ($row = mysqli_fetch_assoc($result)) {
            echo "<tr>";
            echo "<td class='p-2'><a href='load/uploads/nikah/" . $row['akte_kelahiran'] . "'>View</a></td>";
            echo "<td class='p-2'><a href='load/uploads/nikah/" . $row['surat_baptis'] . "'>View</a></td>";
            echo "<td class='p-2'><a href='load/uploads/nikah/" . $row['surat_pemberkatan_perkawinan'] . "'>View</a></td>";
            echo "<td class='p-2'><a href='load/uploads/nikah/" . $row['surat_keterangan_sehat'] . "'>View</a></td>";
            echo "<td class='p-2'><a href='load/uploads/nikah/" . $row['ktp'] . "'>View</a></td>";
            echo "<td class='p-2'><a href='https://wa.me/" . $row['nomer'] . "' class='btn btn-primary'>Chat Wa</a></td>";
            echo "</tr>";
        }

        echo "</table>";
    } else {
        echo "Tidak ada data yang ditemukan.";
    }
} else {
    echo "Error: " . mysqli_error($conn);
}
?>


                        </div>
                    </div>
                    <div class="card-style mb-30">
                        <p>Data Keterangan Pernah Nikah</p>
                        <div class="table-wrapper table-responsive" style="max-height: 360px; overflow-y: scroll;">
                            <?php
                            $query = "SELECT * FROM keterangan_pernah_nikah";
                            $result = mysqli_query($conn, $query);

                            // Mengecek apakah query berhasil dieksekusi
                            if ($result) {
                                // Mengecek apakah ada data yang dihasilkan
                                if (mysqli_num_rows($result) > 0) {
                                    ?>
                                    <table class='table striped-table'>
                                        <thead class="p-3">
                                            <tr>
                                                <th class="p-3">Nama</th>
                                                <th class="p-3">Jenis Kelamin</th>
                                                <th class="p-3">Agama</th>
                                                <th class="p-3">Tanggal</th>
                                                <th class="p-3">Alamat</th>
                                                <th class="p-3">Saksi</th>
                                                <th class="p-3">Nomer</th>
                                            </tr>
                                        </thead>
                                        <tbody class="p-3">
                                            <?php while ($row = mysqli_fetch_assoc($result)): ?>
                                                <tr>
                                                    <td class="p-3">
                                                        <?php echo $row['nama']; ?>
                                                    </td>
                                                    <td class="p-3">
                                                        <?php echo $row['jenis_kelamin']; ?>
                                                    </td>
                                                    <td class="p-3">
                                                        <?php echo $row['agama']; ?>
                                                    </td>
                                                    <td class="p-3">
                                                        <?php echo $row['tanggal']; ?>
                                                    </td>
                                                    <td class="p-3">
                                                        <?php echo $row['alamat']; ?>
                                                    </td>
                                                    <td class="p-3">
                                                        <?php echo $row['saksi']; ?>
                                                    </td>
                                                    <?php echo '<td class="p-3">';
                                                    echo '<a href="https://wa.me/' . $row['nomer']
                                                        . '" class="btn btn-primary">Chat Wa</a>';
                                                    echo '</td>'; ?>
                                                </tr>
                                            <?php endwhile; ?>
                                        </tbody>
                                    </table>
                                    <?php
                                } else {
                                    echo "Tidak ada data yang ditemukan.";
                                }
                            } else {
                                echo "Error: " . mysqli_error($conn);
                            }
                            ?>
                        </div>
                    </div>

                <?php endif; ?>
                <!-- ========== form-elements-wrapper start ========== -->
                <?php if (!$is_admin): ?>
                    <div class="form-elements-wrapper">
                        <div class="row">
                            <div class="col-lg-6">
                                <!-- input style start -->
                                <form action="load/layanannikah.php" method="POST" enctype="multipart/form-data"
                                    class="card-style mb-30">
                                    <h6 class="mb-25">Pengantar Nikah (N1-N6)</h6>
                                    <!-- end input -->
                                    <div class="input-style-2">
                                        <label>Foto Akta Kelahiran</label>
                                        <input type="file" id="akte_kelahiran" name="akte_kelahiran" required />
                                    </div>
                                    <div class="input-style-2">
                                        <label>Foto Surat Keterangan dari Agama</label>
                                        <input type="file" id="surat_baptis" name="surat_baptis" required />
                                    </div>
                                    <!-- end input -->
                                    <div class="input-style-2">
                                        <label>Foto Surat pemberkatan perkawinan dari Agama</label>
                                        <input type="file" id="surat_pemberkatan_perkawinan"
                                            name="surat_pemberkatan_perkawinan" required />
                                    </div>
                                    <div class="input-style-2">
                                        <label>Surat Keterangan Sehat dari Dokter</label>
                                        <input type="file" id="surat_keterangan_sehat" name="surat_keterangan_sehat"
                                            required />
                                    </div>
                                    <div class="input-style-2">
                                        <label>Foto KTP</label>
                                        <input type="file" id="ktp" name="ktp" required />
                                    </div>
                                    <div class="input-style-2">
                                        <label>Nomer ( <span style="color: red;">wajib berawalan 62****</span> )</label>
                                        <input type="number" name="nomer" required />
                                    </div>
                                    <div>
                                        <input class="main-btn primary-btn btn-hover" type="submit" value="Submit">
                                    </div>
                                    <!-- end input -->
                                </form>
                                <!-- end card -->
                                <!-- ======= input switch style end ======= -->
                            </div>
                            <!-- end col -->
                            <div class="col-lg-6">
                                <!-- ======= textarea style start ======= -->
                                <form action="load/keterangan_pernah_nikah.php" method="POST" class="card-style mb-30">
                                    <h6 class="mb-25">Layanan Pindah Datang WNI</h6>
                                    <div class="input-style-1">
                                        <label>Nama</label>
                                        <input type="text" id="nama" name="nama" required placeholder="Nama Lengkap" />
                                    </div>
                                    <div class="input-style-2">
                                        <label>Jenis Kelamin</label>
                                        <select id="jenis_kelamin" name="jenis_kelamin" required class="form-control">
                                            <option value="">Pilih Jenis Kelamin</option>
                                            <option value="Laki-laki">Laki-laki</option>
                                            <option value="Perempuan">Perempuan</option>
                                        </select>
                                    </div>
                                    <div class="input-style-2">
                                        <label>Agama</label>
                                        <input type="text" id="agama" name="agama" required placeholder="Agama" />
                                    </div>
                                    <div class="input-style-2">
                                        <label for="tanggal">Tanggal</label>
                                        <input type="date" id="tanggal" name="tanggal" required>
                                    </div>
                                    <div class="input-style-2">
                                        <label>Alamat</label>
                                        <textarea id="alamat" name="alamat" required
                                            placeholder="Tuliskan alamatmu dengan lengkap!"></textarea>
                                    </div>
                                    <div class="input-style-2">
                                        <label>Saksi</label>
                                        <input type="text" id="saksi" name="saksi" required placeholder="Saksi Pernikahan">
                                    </div>
                                    <div class="input-style-2">
                                        <label>Nomer ( <span style="color: red;">wajib berawalan 62****</span> )</label>
                                        <input type="number" name="nomer" required />
                                    </div>
                                    <div>
                                        <input class="main-btn primary-btn btn-hover" type="submit" name="submit"
                                            value="Upload">
                                    </div>
                                </form>

                                <!-- ======= textarea style end ======= -->

                                <!-- ======= checkbox style start ======= -->
                                <!-- ======= radio style end ======= -->
                            </div>
                            <!-- end col -->
                        </div>
                        <!-- end row -->
                    </div>
                <?php endif; ?>


                <!-- === end menu === -->

            </div>
            <!-- end container -->
        </section>
        <!-- ========== section end ========== -->
        <!-- ========== footer start =========== -->
        <footer class="footer">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-md-6 order-last order-md-first">
                        <div class="copyright text-center text-md-start">
                            <p class="text-sm">
                                Designed and Developed by
                                <a href="https://plainadmin.com" rel="nofollow" target="_blank">
                                    PlainAdmin
                                </a>
                            </p>
                        </div>
                    </div>
                    <!-- end col-->
                    <div class="col-md-6">
                        <div class="
                  terms
                  d-flex
                  justify-content-center justify-content-md-end
                ">
                            <a href="#0" class="text-sm">Term & Conditions</a>
                            <a href="#0" class="text-sm ml-15">Privacy & Policy</a>
                        </div>
                    </div>
                </div>
                <!-- end row -->
            </div>
            <!-- end container -->
        </footer>
        <!-- ========== footer end =========== -->
    </main>
    <script src="../assets/js/bootstrap.bundle.min.js"></script>
    <script src="../assets/js/Chart.min.js"></script>
    <script src="../assets/js/dynamic-pie-chart.js"></script>
    <script src="../assets/js/moment.min.js"></script>
    <script src="../assets/js/fullcalendar.js"></script>
    <script src="../assets/js/jvectormap.min.js"></script>
    <script src="../assets/js/world-merc.js"></script>
    <script src="../assets/js/polyfill.js"></script>
    <script src="../assets/js/main.js"></script>
</body>

</html>
```
