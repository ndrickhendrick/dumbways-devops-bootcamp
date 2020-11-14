Jika saat ini Kamu adalah seorang DevOps di sebuah perusahaan, bagaimana caramu mengamankan server-server tersebut? 
Jawaban :
Cara yang saya lakukan adalah :
1. Melakukan hardening di setiap server dan membatasi akses kebeberapa port yang tidak digunakan.
2. hardening dari sisi apps ygdigunakan, server & database. contoh kecilnya menyembunyikan versi dari web-server dan database yg digunakan, hal ini dilakukan untuk pencegahan.
3. menggunakan firewall bisa fisik atau pun aplikasi firewalld.dan memastikan port" yg digunakan , agar tidak ada celah yg bisa di susupi.
4. memasang antivirus diseluruh server, serta menjadwalkan task untuk scan vulnerability setiap 2 * seminggu.
5. menggunakan cloudflare disisi depan layer apps, kita tahu cloudflare banyak fungsinya yg bisa dimanfaatkan walaupun ada gratisan. seperti rendering ip host, hal ini bisa dilakukan untuk mengecoh hacker.
6. Menggunakan WAF(web Application firewall) & CSF(Config Security Firewall) untuk mengamankan web dari serangan ddos, sql inject, xss, dll.