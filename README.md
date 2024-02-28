# WEB APPLICATION 
Adalah aplikasi yang berjalan di Server dan ditampilkan di Browser Client.
Saat membuat web application, biasanya akan dibagi menjadi 3 bagian : Client, Server, dan Database.

# CONCURENCY & PARALEL 

![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/6bbd8759-559e-4f00-9f88-91e8fdfe964e)

![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/fb79e2e1-f75a-4d07-b936-2fc7786500ef)

![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/970e8346-53f3-4dc6-9d2e-fd703661afcd)

# THREAD 
Program biasanya berjalan dalam sebuah proses, dan proses akan memiliki resource yang independen dengan proses lain. 

Sekarang, sistem operasi tidak hanya bisa menjalankan multiple proses, namun DALAM proses kita bisa menjalankan banyak pekerjaan sekaligus, dinamakan Thread.

Thread membuat proses aplikasi bisa berjalan tidak harus selalu sequential, kita bisa membuat proses aplikasi berjalan menjadi async atau paralel. 

# SYNC VS ASYNC
## SYNC 
Kode program berjalan secara sequential. Semua tahapan ditunggu sampai prosesnya selesai baru akan di eksekusi ke tahapan selanjutnya. 
![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/76dee3c5-e36f-4c1f-9daa-fa87109c1223)

## ASYNC
Kode program kita berjalan dan tidak perlu menunggu eksekusi kode tersebut selesai, kita bisa melanjutkan ke program selanjutnya. 
![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/a0a23cd4-38c0-4d7a-b5d7-6605426deb28)

# THREADPOOL WEB MODEL
Threadpool => untuk melakukan management thread. 
Threadpool merupakan tempat menyimpan thread, ketika kita butuh maka thread akan diambil dari threadpool, ketika sudah selesai maka thread akan dikembalikan ke threadpool.

Dengan threadpool, kita bisa memanfaatkan thread yang sama berkali-kali tanpa harus membuat thread baru terus menerus. 

![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/094929d6-52e2-40e2-a180-3d0161e836b6)


### Threadpool queque

Jika semua thread penuh, kita tidak bisa meminta lagi thread ke threadpool. Kita harus menunggu sampai ada thread yang tidak sibuk. 
Threadpool memiliki tempat untuk menyimpan tugas yang belum dikerjakan oleh thread dinamakan QUEQUE. 

FLOW => task ditampung di queque lalu thread didalam threadpool dijalankan. 

![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/de950eac-b459-4c2a-8328-4525f3ffa738)

### Threadpool Web Model
Dulu pembuatan web application sering menggunakan THREADPOOL MODEL, tapi skrg engga. 

Threadpool model => setiap request yang masuk kw web server akan diproses oleh satu buah thread. Jika ada banyak request yg masuk, semua bisa diproses secara paralel dan akan ditangani oleh thread masing-masing. 
NAMUN threadpool model ini memiliki kekurangan, ketika thread sibuk semua, secara otomatis akan menunggu sampai ada thread yang selesai melakukan tugas sebelumnya. 

Contoh web server yang menggunakan threadpool model => Apache HTTPD, Apache Tomcat. 


# BLOCKING dan NONBLOCKING 

## BLOCKING 
Default program adalah blocking / synchronouns. 

Contoh : membuat kode program untuk membaca file, jika kode kita blocking, maka kita harus menunggu program selesai membaca file baru bisa melanjutkan kode program selanjutnya. 

## NON-BLOCKING 
Async. 

Kode non-blocking akan dieksekusi tanpa harus menunggu kode program tanpa harus menunggu kode program tersebut selesai. 

Ketika memanggil kode non-blocking, biasanya kita perlu mengirim callback untuk dipanggil oleh kode non-blocking tersebut ketika kodenya sudah selesai. 

Contoh non-blocking di JS : AJAX, FetchAPI. 

Di NodeJS, semua fiturnya mendukung kode non-blocking. 

BY DEFAULT NODE JS ADALAH NON-BLOCKING. Ada beberapa yg blocking tp sebisa mungkin nodejs meng-encourage kita untuk menggunakanya secara non-blocking. 

# NODEJS ARCHITECTURE

Event loop => mirip threadpool tapi cuma punya satu thread. Dia hanya mengeksekusi kode program, task nya dikirimkan ke c++ threadpool. 

C++ threadpool => mengeksekusi task. Kalo dah selesai c++ threadpool akan memanggil callback yang diterima oleh event loop. 

Lalu event loop mengirim response ke client.

![image](https://github.com/affodilajF/NodeJS-SelfLearning/assets/130672181/7dd29fce-9cd8-431f-ac23-b87a0b52ab16)



### EVENT LOOP
- Merupakan single thread processes yang digunakan untuk mengeksekusi kode NON-BLOCKINHG.
- Karena single thread, kita harus hati-hati ketika membuat blocking kode, karena bisa memperlambat proses eksekusi kode kita. Bayangin udah blocking, trs single thread lagi. Waduh.
- Tugasnya HANYA menerima dan mengeksekusi kode ke c++ threadpool, jadi, selalu usahakan menggunakan kode nonblocking agar proses blockingnya dikerjakan di c++ threadpool.
- Eventloop hanya menerima response dari c++ threadpool yang dikirim via callback.

### C++ THREADPOOL
- threadpool untuk melakukan pekerjaan (bisa untuk kode blocking)
- LIBUV => library default di NodeJS, secara default menggunakan 4 thread di dalam threadpoolnya.
- Ubah jumlah thread libuv dgn pengaturan environment variable UV_THREADPOOL_SIZE.






