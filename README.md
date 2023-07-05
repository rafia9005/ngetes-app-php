```php
<?php
if(isset($_POST['submit'])) {
    // ...
    
    $target_dir = "uploads/surat_kTH/";
    
    // Buat direktori jika belum ada
    if (!file_exists($target_dir)) {
        mkdir($target_dir, 0777, true);
    }
    
    // Set izin akses pada direktori
    chmod($target_dir, 0777);
    
    // Daftar file yang akan diunggah
    $target_files = array("foto1", "foto3", "foto5");
    $uploaded_files = array();
    
    foreach ($target_files as $file) {
        if (isset($_FILES[$file]) && !empty($_FILES[$file]["name"])) {
            $target_file = $target_dir . basename($_FILES[$file]["name"]);
            if (move_uploaded_file($_FILES[$file]["tmp_name"], $target_file)) {
                $uploaded_files[$file] = $target_file;
            } else {
                echo "Terjadi kesalahan saat mengunggah file " . $file . ".";
                exit;
            }
        }
    }
    
    // ...
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
