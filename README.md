# Git Style Guide

Ini adalah Git Style Guide yang terinspirasi oleh [*How to Get Your Change Into the Linux
Kernel*](https://kernel.org/doc/html/latest/process/submitting-patches.html),
dari [git man pages](http://git-scm.com/doc) dan beberapa praktik yang populer dikalangan komunitas.

Beberapa terjemahan tersedia di berbagai bahasa berikut:

* [Chinese (Simplified)](https://github.com/aseaday/git-style-guide)
* [Chinese (Traditional)](https://github.com/JuanitoFatas/git-style-guide)
* [French](https://github.com/pierreroth64/git-style-guide)
* [Georgian](https://github.com/davidkadaria/git-style-guide)
* [German](https://github.com/runjak/git-style-guide)
* [Greek](https://github.com/grigoria/git-style-guide)
* [Indonesian](https://github.com/refansa/git-style-guide)
* [Italian](https://github.com/vincendep/git-style-guide)
* [Japanese](https://github.com/objectx/git-style-guide)
* [Korean](https://github.com/ikaruce/git-style-guide)
* [Polish](https://github.com/mbiesiad/git-style-guide/tree/pl_PL)
* [Portuguese](https://github.com/guylhermetabosa/git-style-guide)
* [Russian](https://github.com/alik0211/git-style-guide)
* [Spanish](https://github.com/jeko2000/git-style-guide)
* [Thai](https://github.com/zondezatera/git-style-guide)
* [Turkish](https://github.com/CnytSntrk/git-style-guide)
* [Ukrainian](https://github.com/denysdovhan/git-style-guide)

Jika kamu ingin berkontribusi, kamu dipersilahkan! Fork proyek ini dan buka sebuah pull request.

# Daftar Isi

1. [Branches](#branches)
2. [Commits](#commits)
  1. [Pesan](#pesan)
3. [Merging](#merging)
4. [Lain-lain.](#lain-lain)

## Branches

* Pilih nama yang *pendek* dan *deskriptif*:

  ```shell
  # bagus
  $ git checkout -b oauth-migration

  # tidak bagus - terlalu samar
  $ git checkout -b login_fix
  ```

* Pengidentifikasi dari ticket-ticket terkait di dalam sebuah layanan eksternal
  (cth. GitHub issue) juga kandidat yang bagus untuk digunakan dalam nama branch. Sebagai contoh:

  ```shell
  # GitHub issue #15
  $ git checkout -b issue-15
  ```

* Gunakan huruf kecil di nama branch. Pengidentifikasi tiket eksternal
  dengan huruf besar adalah pengecualian yang valid. Gunakan *tanda hubung* untuk memisahkan kata.

  ```shell
  $ git checkout -b new-feature      # bagus
  $ git checkout -b T321-new-feature # tidak bagus (Phabricator task id)
  $ git checkout -b New_Feature      # tidak bagus
  ```

* Saat beberapa orang sedang mengerjakan fitur yang *sama*, mungkin akan lebih nyaman
  untuk mempunyai branch fitur *personal* dan sebuah branch fitur *seluruh tim*.
  Gunakan konvensi penamaan berikut:

  ```shell
  $ git checkout -b feature-a/main   # branch untuk seluruh tim
  $ git checkout -b feature-a/maria  # Personal branch milik Maria
  $ git checkout -b feature-a/nick   # Personal branch milik Nick
  ```

  Gabungkan branch personal kapan saja ke branch tim (Lihat ["Merging"](#merging)).
  Pada akhirnya, branch tim akan digabungkan ke "main".

* Hapus branch Anda dari repositori upstream setelah penggabungan, kecuali ada
  alasan spesifik untuk tidak melakukannya.

  Tip: Gunakan perintah berikut ketika sedang dalam "main", untuk menampilkan branch yang tergabung:

  ```shell
  $ git branch --merged | grep -v "\*"
  ```

## Commits

* Setiap commit harus merupakan satu *perubahan logika* tunggal. Jangan membuat beberapa
  *perubahan logika* dalam satu commit. Sebagai contoh, jika terdapat patch yang memperbaiki sebuah
  bug dan me-optimisasi performa dari sebuah fitur, pisahkan itu menjadi dua commit yang terpisah.

  *Tip: Gunakan `git add -p` untuk menambahkan area-area tertentu dari file-file yang telah
  dimodifikasi secara interaktif.*

* Jangan memisahkan sebuah "perubahan logika" tunggal ke beberapa commit. Sebagai contoh,
  Implementasi dari sebuah fitur dan tes-tes yang berkaitan seharusnya ada didalam
  commit yang sama.

* Commit *lebih awal* dan *lebih sering*. Commit-commit mandiri yang kecil lebih mudah untuk
  dimengerti dan dikembalikan ketika terjadi sesuatu yang salah.

* Commit-commit harus diurutkan secara *logis*. Sebagai contoh, jika *commit X* memerlukan perubahan
  diselesaikan pada *commit Y*, berarti *commit Y* harus datang sebelum *commit X*.

Catatan: Ketika mengerjakan sendiri disebuah branch lokal yang *belum sepenuhnya dipush*, tidak apa-apa
untuk menggunakan commit-commit sebagai cuplikan sementara dari pengerjaan-mu. Namun, aturan-aturan 
tadi masih berlaku kalau kamu harus mengaplikasikan seluruh perubahan diatas *sebelum* menge-push-nya.

### Pesan

* Gunakan editor, bukan terminal, ketika menulis sebuah pesan commit:

  ```shell
  # bagus
  $ git commit

  # tidak bagus
  $ git commit -m "Quick fix"
  ```

  Meng-commit dari terminal mendorong sebuah pemikiran untuk harus memasukkan segalanya
  dalam sebuah baris tunggal yang mana biasanya menghasilkan pesan commit yang tidak informatif dan ambigu.

* Baris kesimpulan (yaitu berarti baris pertama dari sebuah pesan) harus
  *deksriptif* dan *ringkas*. Idealnya, harus tidak lebih dari
  50 karakter. Harus di-kapitalisasi dan ditulis dalam bentuk kata kerja perintah
  masa kini. Harus tidak berakhiran dengan sebuah titik karena itu secara efektif adalah
  *judul* dari commit-nya:

  ```shell
  # bagus - kata kerja perintah masa kini, di-kapitalisasi, lebih sedikit dari 50 karakter
  Mark huge records as obsolete when clearing hinting faults

  # tidak bagus
  fixed ActiveModel::Errors deprecation messages failing when AR was used outside of Rails.
  ```

* Setelah itu harus disertai dengan baris kosong di-ikuti dengan
  deskripsi yang lebih menyeluruh. Harus dibungkus menjadi *72 karakter* dan
  menjelaskan *mengapa* perubahan itu dibutuhkan, *bagaimana* itu mengatasi masalah yang ada
  dan apa *efek samping* yang mungkin itu punya.

  Itu juga harus memberikan beberapa penunjuk apa saja yang berkaitan dengan sumber daya tersebut
  (cth. link ke issue yang bersangkutan di sebuah bug tracker):

  ```text
  Kesimpulan perubahan pendek (50 karakter atau kurang)

  Teks penjelasan lebih detail, jika diperlukan. Bungkus menjadi
  72 karakter. Dalam beberapa konteks, baris pertama diperlakukan
  sebagai subjek dari sebuah email dan sisanya sebagai teks badan.
  Baris yang kosong memisahkan kesimpulan dengan badan itu sangat
  penting (kecuali kamu menghilangkan badannya secara menyeluruh);
  alat seperti rebase bisa membingungkan jika kamu menjalankan
  keduanya secara bersamaan.

  Paragraf selanjutnya didatangi setelah baris kosong.

  - Beberapa poin-poin juga oke

  - Gunakan tanda hubung atau tanda bintang untuk poinnya,
    disertai dengan spasi tunggal, dengan baris kosong diantaranya

  Penunjuk ke sumber daya yang bersangkutan dapat berfungsi sebagai
  footer untuk pesan commit-mu. Ini adalah contoh yang mereferensikan issue
  dalam sebuah bug tracker:

  Resolves: #56, #78
  See also: #12, #34

  Source: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  ```

  Akhirnya, ketika menulis sebuah pesan commit, pikir tentang apa yang perlu kamu
  ketahui jika kamu kembali melihat commit itu dalam se-tahun dari sekarang.

* Jika sebuah *commit A* bergantung pada *commit B*, ketergantungan tersebut harus
  dinyatakan dalam pesan dari *commit A*. Gunakan SHA1 ketika mereferensikan ke commit.

  Demikian pula, jika *commit A* memperbaiki sebuah bug yang di bawa oleh *commit B*,
  itu juga harus dinyatakan dalam pesan dari *commit A*.

* Jika sebuah commit akan di-squashed ke commit lain, masing-masing gunakan flags `--squash` dan
  `--fixup`, untuk membuat niat yang jelas:

  ```shell
  $ git commit --squash f387cab2
  ```

  *(Tip: Gunakan flag `--autosquash` saat rebasing. Commit yang sudah ditandai akan
  ter-squashed secara otomatis.)*

## Merging

* **Jangan menulis ulang sejarah commit yang telah dipublikasikan** Sejarah history
  itu berharga dengan sendirinya dan sangatlah penting untuk dapat mengetahui *apa yang
  sebenarnya terjadi*. Mengubah sejarah yang telah dipublikasi adalah sumber utama masalah
  untuk siapa pun yang sedang mengerjakan proyek.

* Namun, ada beberapa kasus dimana menulis ulang sejarah adalah sah-sah saja. Ini adalah
  saat:

  * Kamu adalah orang satu-satunya yang sedang bekerja dalam branch dan itu tidak sedang review.

  * Kamu ingin membersihkan branch-mu (cth. commit yang di-squash) dan/atau rebase branch tersebut
    ke "main" untuk di-merge nanti.
    
  Meskipun demikian, *jangan pernah menulis ulang sejarah dari branch "main"* atau
  branch spesial lain (yaitu digunakan oleh server produksi atau CI).

* Jaga agar sejarahnya tetap *bersih* dan *simpel*. *Tepat sebelum kamu merge* branch-mu:

    1. Pastikan itu sesuai dengan gaya panduan dan melakukan aksi apapun yang dibutuhkan
       agar itu tidak (squash/menyusun ulang commit, mengubah kata pesan, dll.)

    2. Rebase ke branch yang akan digabungkan:

       ```shell
       [my-branch] $ git fetch
       [my-branch] $ git rebase origin/main
       # lalu gabung
       ```
 
       Ini menghasilkan sebuah branch yang dapat diterapkan langsung ke akhir dari
       branch "main" dan menghasilkan sejarah yang sangat simpel.

       *(Note: Strategy ini lebih baik untuk proyek dengan masa hidup branch yang pendek.
       Jika tidak, lebih baik menggabungkan branch "main" lebih sering daripada
       me-rebase kedalamnya.)*

* Jika branch-mu memasukkan lebih dari satu commit, jangan menggabungkannya
  dengan fast-forward:

  ```shell
  # bagus - pastikan commit yang digabung telah terbuat
  $ git merge --no-ff my-branch

  # tidak bagus
  $ git merge my-branch
  ```

## Lain-lain.

* Ada banyak alur kerja dan masing-masing memiliki kelebihan dan kekurangannya tersendiri.
  Apakah suatu alur kerja sesuai dengan kasus-mu, tergantung dengan tim, proyek, dan prosedur
  pengembanganmu sendiri.

  Meskipun demikian, sebenarnya sangatlah penting untuk *memilih* suatu alur kerja dan
  berpegang teguh padanya.

* *Bersikaplah konsisten.* Ini menyangkut pada alur kerja tapi juga meluas ke hal-hal
  lain seperti pesan commit, nama branch dan tag. Memiliki gaya yang konsisten sepanjang
  repositori membuatnya lebih mudah untuk memahami apa yang terjadi dari melihat log,
  pesan commit, dll.
  
* *Tes sebelum kamu push.* Jangan menge-push pekerjaan yang setengah-setengah.

* Gunakan [annotated tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_annotated_tags)
  untuk menandai rilis atau poin penting lainnya di sejarah commit. Pilihlah
  [lightweight tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_lightweight_tags)
  untuk penggunaan personal, seperti untuk bookmark commit untuk referensi di masa depan.

* Jagalah repositori-mu dalam kondisi yang bagus dengan melakukan tugas-tugas pemeliharaan
  secara berkala:

  * [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  * [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  * [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)

# License

![cc license](http://i.creativecommons.org/l/by/4.0/88x31.png)

This work is licensed under a [Creative Commons Attribution 4.0
International license](https://creativecommons.org/licenses/by/4.0/).

# Credits

Agis Anastasopoulos / [@agisanast](https://twitter.com/agisanast) / http://agis.io
... and [contributors](https://github.com/agis-/git-style-guide/graphs/contributors)!

# Translator
Muhammad Refansa Ali Muzky / [@refansa](https://github.com/refansa)
