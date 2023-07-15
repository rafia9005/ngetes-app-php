```php
<?php
// Include file konfigurasi
include '../../config/config.php';

// Memeriksa apakah form telah di-submit
if ($_SERVER["REQUEST_METHOD"] == "POST") {
  // Mendapatkan nilai dari form
  $name = $_POST['name'];
  $akte_kelahiran = $_FILES["akte_kelahiran"]["name"];
  $surat_baptis = $_FILES["surat_baptis"]["name"];
  $surat_pemberkatan_perkawinan = $_POST['surat_pemberkatan_perkawinan'];
  $surat_keterangan_sehat = $_FILES["surat_keterangan_sehat"]["name"];
  $ktp = $_FILES["ktp"]["name"];
  $nomer = $_POST['nomer'];

  // Memindahkan file yang di-upload ke folder yang diinginkan
  $targetDir = "uploads/nikah/";
  move_uploaded_file($_FILES["akte_kelahiran"]["tmp_name"], $targetDir . basename($akte_kelahiran));
  move_uploaded_file($_FILES["surat_baptis"]["tmp_name"], $targetDir . basename($surat_baptis));
  move_uploaded_file($_FILES["surat_keterangan_sehat"]["tmp_name"], $targetDir . basename($surat_keterangan_sehat));
  move_uploaded_file($_FILES["ktp"]["tmp_name"], $targetDir . basename($ktp));

  // Menghubungkan ke database
  include '../../config/config.php';

  // Menyimpan data ke database
  $sql = "INSERT INTO keterangan_nikah (name, akte_kelahiran, surat_baptis, surat_pemberkatan_perkawinan, surat_keterangan_sehat, ktp, nomer)
          VALUES ('$name','$akte_kelahiran', '$surat_baptis', '$surat_pemberkatan_perkawinan', '$surat_keterangan_sehat', '$ktp', '$nomer')";
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
