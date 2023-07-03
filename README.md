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
        <li class="nav-item nav-item-has-children">
          <a href="#" aria-expanded="false" aria-label="Toggle navigation">
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
        <li class="nav-item nav-item-has-childre">
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
$sql = "SELECT * FROM surat_keterangan_pindah";
$result = $conn->query($sql);

// Jika terdapat data pada tabel, tampilkan dalam bentuk tabel
if ($result->num_rows > 0) {
  echo "<table class='table striped-table'>";
  echo "<tr><th class='p-3'>Foto SKPWNI</th><th class='p-3'>Foto KK</th><th class='p-3'>Foto KTP</th><th class='p-3'>Foto Surat Nikah</th><th class='p-3'>Nomer</th><th>Aksi</th></tr>";
  while ($row = $result->fetch_assoc()) {
    echo "<tr class='p-3'>";
    echo "<td class='p-3'><a href='load/" . $row["foto_SKPWNI"] . "'>View</a></td>";
    echo "<td class='p-3'><a href='load/" . $row["foto_KK"] . "'>View</a></td>";
    echo "<td class='p-3'><a href='load/" . $row["foto_KTP"] . "'>View</a></td>";
    echo "<td class='p-3'>";
    if ($row["foto_suratnikah"] != "") {
      echo "<a href='load/" . $row["foto_suratnikah"] . "'>View</a>";
    } else {
      echo "Foto tidak ada";
    }
    echo "</td>";
    echo "<td class='p-3'><a href='https://wa.me/" . $row["nomer"] . "' class='btn btn-primary'>Chat</a></td>";
    echo "<td class='p-3'><form method='post' action='load/delete_pindah.php'><input type='hidden' name='id' value='" . $row['id'] . "'><button type='submit' class='btn btn-danger'>Delete</button></form></td></tr>";
    echo "</tr>";
  }
  echo "</table>";
} else {
  echo "Tidak ada data yang ditemukan.";
}
?>

            </div>
          </div>
          <div class="card-style mb-30">
            <p>Data Pindah Datang WNI</p>
            <div class="table-wrapper table-responsive" style="max-height: 360px; overflow-y: scroll;">
              <?php
              $sql = "SELECT * FROM surat_keterangan_datang_wni";
              $result = mysqli_query($conn, $sql);

              // Tampilkan data dalam tabel HTML
              if (mysqli_num_rows($result) > 0) {
                echo "<table class='table striped-table'>";
                echo "<tr>
          <th class='p-2'>ID</th>
          <th class='p-2'>Foto KK</th>
          <th class='p-2'>Foto KTP</th>
          <th class='p-2'>Foto Akta</th>
          <th class='p-2'>Golongan Darah</th>
          <th class='p-2'>Nomer</th>
        </tr>";
                while ($row = mysqli_fetch_assoc($result)) {
                  echo "<tr>
            <td class='p-2'>" . $row["id"] . "</td>
            <td class='p-2'><a href='load/" . $row["foto_kk"] . "'>View</a></td>
            <td class='p-2'><a href='load/" . $row["foto_ktp"] . "'>View</a></td>
            <td class='p-2'><a href='load/" . $row["foto_akta"] . "'>View</a></td>
            <td class='p-2'>" . $row["golongan_darah"] . "</td>
            <td class='p-2'><a href='https://wa.me/" . $row["nomer"] . "' class='p-2 btn btn-primary'>Chat Wa</a></td>
          </tr>";
                }
                echo "</table>";
              } else {
                echo "Tidak ada data yang ditemukan";
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
                <!-- input style start --><form action="load/surat_keterangan_pindah.php" method="POST" enctype="multipart/form-data" class="card-style mb-30">
  <h6 class="mb-25">Layanan Keterangan Pindah</h6>
  <div class="input-style-1">
    <label>Foto Surat SKPWNI</label>
    <input type="file" name="foto_SKPWNI" id="foto_SKPWNI" required />
  </div>
  <!-- end input -->
  <div class="input-style-2">
    <label>Foto Kartu Keluarga</label>
    <input type="file" name="foto_KK" id="foto_KK" required />
  </div>
  <div class="input-style-2">
    <label>Foto KTP</label>
    <input type="file" name="foto_KTP" id="foto_KTP" required />
  </div>
  <!-- end input -->
  <div class="input-style-2">
    <label>Foto Surat Nikah <span style="color: red;">( Tidak Wajib )</span></label>
    <input type="file" name="foto_suratnikah" id="foto_suratnikah" />
  </div>
  <div class="input-style-2">
    <label>Nomer HP ( <span style="color: red;">wajib berawalan 62****</span> )</label>
    <input type="number" name="nomer" placeholder="nomer active" />
  </div>
  <div>
    <input class="main-btn primary-btn btn-hover" type="submit" value="Upload">
  </div>
  <!-- end input -->
</form>

                <!-- end card -->
                <!-- ======= input style end ======= -->

                <!-- ======= select style start ======= -->
               
                <!-- end card -->
                <!-- ======= select style end ======= -->

                <!-- ======= input switch style end ======= -->
              </div>
              <!-- end col -->
              <div class="col-lg-6">
                <!-- ======= textarea style start ======= -->
                <form action="load/surat_pindah_wni.php" method="POST" enctype="multipart/form-data"
                  class="card-style mb-30">
                  <h6 class="mb-25">Layanan Pindah Datang WNI</h6>
                  <div class="input-style-1">
                    <label>Foto KK</label>
                    <input type="file" name="foto_kk" required />
                  </div>
                  <!-- end input -->
                  <div class="input-style-2">
                    <label>Foto KTP</label>
                    <input type="file" name="foto_ktp" required />
                  </div>
                  <div class="input-style-2">
                    <label>Foto Akta Kelahiran</label>
                    <input type="file" name="foto_akta" required />
                  </div>
                  <div class="input-style-2">
                    <label>Golongan Darah</label>
                    <select name="golongan_darah" id="golongan_darah" class="form-control">
                      <option value="">- Pilih Golongan Darah -</option>
                      <option value="A+">A+</option>
                      <option value="A-">A-</option>
                      <option value="B+">B+</option>
                      <option value="B-">B-</option>
                      <option value="O+">O+</option>
                      <option value="O-">O-</option>
                      <option value="AB+">AB+</option>
                      <option value="AB-">AB-</option>
                    </select><br><br>
                  </div>
                  <div>
                  <div class="input-style-2">
                    <label>Nomer ( <span style="color: red;">wajib berawalan 62****</span> )</label>
                    <input type="number" name="nomer" required />
                  </div>
                    <input class="main-btn primary-btn btn-hover" type="submit" name="submit" value="Simpan">
                  </div>
                  <!-- end input -->
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
