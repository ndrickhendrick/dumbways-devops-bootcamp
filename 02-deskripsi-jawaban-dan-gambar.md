untuk mencari sebuah file dengan kondisi hanya mengetahui isi filenya saja, kita dapat menggunakan command find atau grep, serta command lainnya.
namun biasanya saya menggunakan command find dikombinasikan dengan grep. berikut saya lampirkan contohnya di screenshoot.

berikut contohnya :
1. saya ingin mencari lokasi dari file log dengan isi data yang mengandung kata berikut : "controller=Api::V1::AccountValidationsController".
2. untuk range filenya di tanggal-bulan-dan tahun berikut : 2019-07-01 s/d 2019-07-31
3. kemudian saya membuat satu file shellscript dengan nama 1.sh, file ini berisikan script dibawah ini :
for i in `find / -name "*puma-api*" -type f -newermt "2019-07-01 00:00:01" \! -newermt "2019-07-31 23:59:59"`; do j=$(echo $i| sed 's/\.\///g'); echo $i; zgrep -A3 -B3 "controller=Api::V1::AccountValidationsController" $i; done >> /home/hendrick/OBS-1512/puma-api-07.log
4. saya membuat penampungan file berlokasi di done >> /home/hendrick/OBS-1512/puma-api-07.log, file puma-api-07.log ini akan menyimpan semua hasil log yg didapat .
5. file 1.sh saya executable(chmod +x) dan nantinya hasilnya akan di lempar ke file puma-api-07.log 
6. file tersebut kita dapat melihat isi dari log file dan lokasinya. silahkan di check pada screenshootnya.
