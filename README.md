```php
<?php
include '../../config/config.php';

$id = $_POST['id'];

$sql = "DELETE FROM surat_keterangan_pindah WHERE id = $id";
if(mysqli_query($conn, $sql))
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
