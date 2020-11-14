Jelaskan perbedaan mencolok antara Docker dengan VMware, serta berikan penjelasan kapan kita harus menggunakan Docker dan VMware? BOBOT MAX: 5
Jawaban :
Perbedaan dasar antara VM dan Docker adalah :
1. VM menggunakan keseluruhan resource hardware yang disediakan oleh host,
sehingga jika kita asumsikan maka sistem operasi telah menjalankan 2 OS. Sedangkan dalam Docker, docker hanya menjalankan aplikasi tertentu,
hal ini membuat penggunaan resource hardware lebih sedikit. (dapat dilihat pada gambar 04-file-1-perbedaan-docker-&-vm.png).
2. virtual machine(VM) menggunakan kernel tersendiri bagi tiap operating systemnya, hal ini tentu saja akan memberatkan operating system pembawanya. 
Berbeda dengan docker, dimana kernel yang digunakan adalah bagian(shared) operating system indukannya.
3. Flexibilitas resource hardware yang berbeda, pada VM resource hardware telah didefenisikan untuk vm-a , vm-b tidak dapat menggunakan resource hardware tersebut.
pada docker, jika ada resource container yang idle maka container yang aktif dapat memanfaatkan resource hardware milik kontainer yang sedang idle tersebut. sehingga lebih flexible pemanfaatan dan penggunaan sharingnya. 