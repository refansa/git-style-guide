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

* Baris kesimpulan (yang mana berarti baris pertama dari sebuah pesan) harus
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

  Ultimately, when writing a commit message, think about what you would need
  to know if you run across the commit in a year from now.

* If a *commit A* depends on *commit B*, the dependency should be
  stated in the message of *commit A*. Use the SHA1 when referring to
  commits.

  Similarly, if *commit A* solves a bug introduced by *commit B*, it should
  also be stated in the message of *commit A*.

* If a commit is going to be squashed to another commit use the `--squash` and
  `--fixup` flags respectively, in order to make the intention clear:

  ```shell
  $ git commit --squash f387cab2
  ```

  *(Tip: Use the `--autosquash` flag when rebasing. The marked commits will be
  squashed automatically.)*

## Merging

* **Do not rewrite published history.** The repository's history is valuable in
  its own right and it is very important to be able to tell *what actually
  happened*. Altering published history is a common source of problems for
  anyone working on the project.

* However, there are cases where rewriting history is legitimate. These are
  when:

  * You are the only one working on the branch and it is not being reviewed.

  * You want to tidy up your branch (eg. squash commits) and/or rebase it onto
    the "main" in order to merge it later.

  That said, *never rewrite the history of the "main" branch* or any other
  special branches (ie. used by production or CI servers).

* Keep the history *clean* and *simple*. *Just before you merge* your branch:

    1. Make sure it conforms to the style guide and perform any needed actions
       if it doesn't (squash/reorder commits, reword messages etc.)

    2. Rebase it onto the branch it's going to be merged to:

       ```shell
       [my-branch] $ git fetch
       [my-branch] $ git rebase origin/main
       # then merge
       ```

       This results in a branch that can be applied directly to the end of the
       "main" branch and results in a very simple history.

       *(Note: This strategy is better suited for projects with short-running
       branches. Otherwise it might be better to occassionally merge the
       "main" branch instead of rebasing onto it.)*

* If your branch includes more than one commit, do not merge with a
  fast-forward:

  ```shell
  # good - ensures that a merge commit is created
  $ git merge --no-ff my-branch

  # bad
  $ git merge my-branch
  ```

## Misc.

* There are various workflows and each one has its strengths and weaknesses.
  Whether a workflow fits your case, depends on the team, the project and your
  development procedures.

  That said, it is important to actually *choose* a workflow and stick with it.

* *Be consistent.* This is related to the workflow but also expands to things
  like commit messages, branch names and tags. Having a consistent style
  throughout the repository makes it easy to understand what is going on by
  looking at the log, a commit message etc.

* *Test before you push.* Do not push half-done work.

* Use [annotated tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_annotated_tags)
  for marking releases or other important points in the history. Prefer
  [lightweight tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging#_lightweight_tags)
  for personal use, such as to bookmark commits for future reference.

* Keep your repositories at a good shape by performing maintenance tasks
  occasionally:

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
