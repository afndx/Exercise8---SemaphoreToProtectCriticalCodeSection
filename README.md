# Kontrol LED STM32 dengan FreeRTOS
Proyek ini menunjukkan penggunaan FreeRTOS untuk manajemen tugas pada mikrokontroler STM32 untuk mengendalikan beberapa LED dengan tugas yang disinkronkan. Program ini mengelola berbagai tugas LED seperti kedipan LED Hijau, Merah, dan Kuning, dengan akses ke sumber daya bersama yang dikendalikan menggunakan semaphore. Program ini juga mensimulasikan akses sumber daya dan menangani masalah konkuren menggunakan semaphore untuk memastikan akses yang aman.

## Fitur
- Multi-tasking dengan FreeRTOS: Program ini memanfaatkan beberapa tugas FreeRTOS untuk mengelola LED dan sumber daya bersama.
- Semaphore untuk Manajemen Sumber Daya Kritis: Semaphore (CriticalResourceSemaphoreHandle) digunakan untuk memastikan hanya satu tugas yang dapat mengakses sumber daya bersama pada satu waktu.
- Pola Kedipan LED: Pola kedipan LED yang berbeda untuk LED Hijau, Merah, dan Kuning dengan penundaan yang dapat disesuaikan.
- 
## Tugas
- GreenLEDTask: Tugas ini menyalakan LED hijau (terhubung ke pin GPIO 0), mensimulasikan akses ke sumber daya bersama, dan kemudian mematikan LED tersebut.
- RedLEDTask: Mirip dengan GreenLEDTask, tetapi mengendalikan LED merah (terhubung ke pin GPIO 1).
- YellowLEDTask: Tugas ini mengubah status LED kuning (terhubung ke pin GPIO 2) dengan frekuensi 10 Hz.
- Penggunaan Semaphore: Semaphore digunakan untuk mengendalikan akses ke sumber daya bersama (accessSharedData function). Ini mensimulasikan bagian kritis dalam program di mana beberapa tugas mungkin mencoba mengakses sumber daya pada waktu yang sama.
## Implementasi Semaphore
- CriticalResourceSemaphoreHandle dibuat dengan satu izin (osSemaphoreCreate), memastikan bahwa hanya satu tugas yang dapat mengakses sumber daya bersama pada satu waktu.
- Tugas memperoleh semaphore sebelum mengakses sumber daya bersama dan melepaskannya setelah selesai, memastikan akses yang aman dan mencegah konflik data.
## Pin GPIO
- GPIOA Pin 0: LED Hijau
- GPIOA Pin 1: LED Merah
- GPIOA Pin 2: LED Kuning
- GPIOA Pin 3: LED Biru (digunakan untuk menunjukkan konflik selama akses sumber daya)
## Alur Program Utama
- Fungsi utama menginisialisasi perangkat keras STM32 dan periferal (GPIO, FreeRTOS, dll.).
- Tiga tugas dibuat untuk mengendalikan LED (GreenLEDTask, RedLEDTask, dan YellowLEDTask).
- Tugas-tugas ini berjalan secara bersamaan, mengelola status LED berdasarkan penundaan waktu yang ditentukan.
- CriticalResourceSemaphoreHandle memastikan bahwa fungsi accessSharedData hanya diakses oleh satu tugas pada satu waktu, mencegah konflik.
## Fungsi
- StartDefaultTask: Ini adalah tugas default, yang dibuat untuk menginisialisasi sistem dan memulai penjadwal FreeRTOS.
- green_led, red_led, dan yellow_led: Fungsi-fungsi ini mengimplementasikan perilaku dari tugas kontrol LED masing-masing.
- accessSharedData: Fungsi ini mensimulasikan akses ke sumber daya bersama. LED biru (GPIO pin 3) akan menyala jika terjadi konflik saat mengakses sumber daya.
- SimulateReadWriteOperation: Fungsi ini mensimulasikan waktu pemrosesan (sekitar 500ms) selama akses ke sumber daya.

## Demo
- exercise 8 WaitTimeMilisecond 1001

https://github.com/user-attachments/assets/bd9a1aa7-6b9b-458f-adbb-7118626a8876

-exercise 8 WaitTimeMilisecond 0



https://github.com/user-attachments/assets/b505d9e5-f7fe-48eb-b68d-c05f13d5a689


