# Java-PAC-MAN-Remastered--Kelompok-PBO-9-
PAC-MAN (Java Swing) - Kelompok PBO 9
======================================

Game Pac-Man klasik yang dibuat dengan Java (Swing / Java2D) sebagai tugas
mata kuliah Pemrograman Berorientasi Objek (PBO). Seluruh grafis digambar
langsung dengan Java2D dan seluruh suara disintesis lewat kode saat program
dimulai, sehingga game tidak membutuhkan berkas gambar maupun audio eksternal
dan tidak memakai pustaka tambahan.


FITUR
-----
- Dua pilihan peta: EDEN (nuansa taman siang hari) dan SPACESHIP (ruang angkasa).
- Tiga tingkat kesulitan: EASY, MEDIUM, dan DIFFICULT (memengaruhi kecepatan
  hantu dan durasi efek power pellet).
- Empat hantu dengan strategi pengejaran berbeda (polimorfisme):
    Ghost1 (merah)  : mengejar langsung posisi Pac-Man.
    Ghost2 (biru)   : menghadang, menargetkan petak di depan arah hadap Pac-Man.
    Ghost3 (ungu)   : mengejar bila jauh, kembali ke sudut bila terlalu dekat.
    Ghost4 (oranye) : mengejar bila dekat, kembali ke sudut bila terlalu jauh.
- Terowongan kiri-kanan pada peta yang memilikinya (Pac-Man dan hantu bisa tembus).
- Item di labirin:
    Pellet        : +10 poin.
    Power Pellet  : +50 poin, Pac-Man lebih cepat dan hantu menjadi frightened
                    sehingga dapat dimakan (+200 poin per hantu).
    Fruit         : +100 poin dan menambah satu nyawa.
    Poison        : memperlambat Pac-Man untuk beberapa saat.
    Ice Cube      : membekukan seluruh hantu untuk beberapa saat.
- Pac-Man memulai dengan 3 nyawa.
- Skor tertinggi (high score) tersimpan otomatis di berkas lokal "highscore.dat".
- Efek suara, sirene latar, jingle, dan musik beranda; status mute tersimpan.
- Menu beranda, overlay jeda / menang / kalah, dan panel "Cara bermain".


INOVASI
-------
Dibandingkan Pac-Man klasik, program ini menambahkan:
1. Item di luar versi klasik: Poison (memperlambat Pac-Man) dan Ice Cube
   (membekukan seluruh hantu) yang menambah unsur strategi.
2. Buah yang selain memberi skor juga menambah satu nyawa.
3. Terowongan kiri-kanan dengan efek suara dan aksen visual khusus.
4. Dua peta dengan tema visual berbeda: Eden (taman siang hari) dan
   Spaceship (ruang angkasa berbintang).
5. Tiga tingkat kesulitan (EASY, MEDIUM, DIFFICULT) yang mengubah kecepatan
   hantu dan durasi power pellet.
6. Audio yang seluruhnya disintesis lewat kode (efek, sirene, jingle, musik),
   tanpa berkas audio eksternal.
7. Gerakan mulus: logika berjalan per petak, tampilan menginterpolasi posisi
   piksel sehingga tidak patah-patah.
8. Antarmuka lengkap (beranda, jeda, menang, kalah, panel "Cara bermain") yang
   bisa dioperasikan lewat mouse maupun keyboard.
9. Arsitektur MVC dan pola Observer sehingga logika game tidak bergantung
   pada audio.


KONTROL
-------
Panah / W A S D   : Gerakkan Pac-Man
P / Esc           : Jeda dan lanjutkan
Tab / Enter       : Pindah dan pilih tombol di menu (mouse juga bisa dipakai)
N                 : Nyalakan / matikan suara
Pintasan beranda  : 1 = peta EDEN, 2 = peta SPACESHIP,
                    E = Easy, M = Medium, F = Difficult


CARA MENJALANKAN
----------------
Prasyarat: JDK (Java Development Kit), disarankan versi 11 atau lebih baru.

1. Masuk ke folder proyek (folder yang berisi folder "src").

2. Kompilasi seluruh kode sumber.

   Linux / macOS:
       mkdir -p out
       javac -encoding UTF-8 -d out $(find src -name "*.java")

   Windows (Command Prompt):
       mkdir out
       dir /s /b src\*.java > sources.txt
       javac -encoding UTF-8 -d out @sources.txt

3. Jalankan game:
       java -cp out com.stis.pacman.Main

Proyek juga dapat dibuka langsung di IDE (IntelliJ IDEA, Eclipse, NetBeans)
dengan folder "src" sebagai source root, lalu jalankan kelas
com.stis.pacman.Main.


STRUKTUR PROYEK
---------------
Proyek memakai pola MVC dengan pola Observer untuk audio.

src/com/stis/pacman/
  Main.java      Titik masuk aplikasi
  model/         Entitas dan data permainan: Maze, Entity, PacMan, Ghost (Ghost1-4),
                 item (Pellet, PowerPellet, Fruit, Poison, IceCube), Difficulty,
                 GameState, GameEvent, GameConfig
  view/          Tampilan: GameWindow, GamePanel, MenuScreen, OverlayScreen,
                 UiButton, UiTheme, MazeTheme
  controller/    Logika permainan: GameEngine (game loop), InputHandler,
                 CollisionManager, ScoreManager, GameEventListener
  audio/         Sintesis dan pemutaran suara: SoundManager, SoundFactory, Mixer,
                 Music, Dsp, AudioOutput


KONSEP PBO YANG DITERAPKAN
--------------------------
- Abstraksi dan pewarisan : Entity -> PacMan, Ghost, CollectibleItem
- Polimorfisme            : Ghost1-4 (getTargetTile) dan seluruh item (efek saat dimakan)
- Enkapsulasi             : atribut private/protected dengan getter dan setter
- Pola Observer           : GameEngine mengirim GameEvent ke GameEventListener
                            (SoundManager) sehingga logika game tidak bergantung pada audio


CATATAN
-------
- Bila perangkat suara tidak tersedia, game tetap berjalan normal tanpa suara.
- Berkas "highscore.dat" dibuat otomatis di folder tempat game dijalankan.


ANGGOTA KELOMPOK
----------------
(isi nama dan NIM anggota Kelompok PBO 9 di sini)
