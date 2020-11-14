Jika kamu menjadi seorang DevOps di sebuah perusahaan dan kamu ditugaskan untuk memonitoring server, tools apa saja yang akan kamu gunakan serta berikan keuntungan menggunakan tools tersebut?  BOBOT MAX: 5
Jawaban :
tools yang akan saya gunakan adalah Grafana + Prometheus
Keuntungan menggunakan grafana adalah open-source, sangat mudah di implementasikan, dan banyak source yang tersedia untuk pengembangan monitoring tools tersebut.
Grafana juga mudah di integrasikan dengan platform lain , seperti slack, pagerduty(untuk notify call), integrate ke email, telegram, dll. Grafana ini daapat di implementasikan di VM, K8S, docker ataupun virtualisasi lainnya.
Grafana dapat memonitoring banyak hal, bisa dari server, firewall, link isp, transaksi serta untuk database.dan saya baca sangat banyak digunakan oleh perusahaan-perusahan besar/kceil.
prometheus di gunakan untuk menampung data(datasource)dari semua exporter yang ada disetiap server.penggunaan prometheus bisa juga di ubah dengan menggunakan graphite, apabila kita ingin mendapatkan graphik yg cocok untuk ratus ribuan data trx dalam detik. Prometheus bisa di kombinasikan dengan alertmanager untuk monitoring, jadi apabila terjadi masalah / issue yang anomaly, maka dapat secara langsng ke trigger alert.

Monitoring tools lain yang digunakan adalah nagios,kibana, cacti, ganglia.