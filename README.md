# Peminjaman Ruangan
# Teknologi
- Frontend: React
- Backend: .NET Web API
- Database: SQL Server (Docker)
- Orkestrasi: Docker Compose

# Struktur Service
| Service  | Port Host | Keterangan         |
| -------- | --------- | ------------------ |
| frontend | **5174**  | Aplikasi web       |
| backend  | **5112**  | REST API + Swagger |
| db       | **1433**  | SQL Server Docker  |

# Cara Menjalankan Project
1. Jalankan semua container
    Dari folder yang berisi `docker-compose.yml`:
    docker compose up -d

Setelah selesai:
- Frontend → [http://localhost:5174](http://localhost:5174)
- Backend Swagger → [http://localhost:5112/swagger](http://localhost:5112/swagger)

2. Menjalankan pertama kali (jika database belum ada)
    Masuk ke folder backend (.csproj) lalu jalankan:
    dotnet ef database update

Perintah ini akan:
- membuat database PeminjamanRuanganDB di SQL Server Docker
- membuat seluruh tabel dari migration

Setelah itu restart backend: docker compose restart backend

# Menghentikan Project
    docker compose down

Database tidak hilang karena disimpan di Docker volume.

# Jika Mengubah Code
Gunakan build ulang: docker compose up --build -d

#  Reset Database dari Nol (Opsional)
    docker compose down -v

Lalu jalankan lagi:
docker compose up -d
dotnet ef database update

# Catatan Penting
## Connection String Backend (Docker)
Backend HARUS menggunakan nama service database:
    Server=peminjaman-db,1433;Database=PeminjamanRuanganDB;User Id=sa;Password=YourPassword123;TrustServerCertificate=True
Jangan pakai localhost di dalam container Docker.


# Ringkasan Perintah Penting

| Kebutuhan            | Perintah                       |
| -------------------- | ------------------------------ |
| Jalankan project     | `docker compose up -d`         |
| Stop project         | `docker compose down`          |
| Build ulang          | `docker compose up --build -d` |
| Buat DB pertama kali | `dotnet ef database update`    |
| Reset DB             | `docker compose down -v`       |
