# PostgreSQL dan pgAdmin

Docker Compose di folder ini menjalankan PostgreSQL 15 dan pgAdmin 4 pada jaringan bridge `postgres`.

## Layanan

| Layanan | Nama container | Image | Port host |
|---------|----------------|-------|-----------|
| PostgreSQL | `postgres_HARY` | `postgres:15` | `22063` |
| pgAdmin | `pgadmin_HARY` | `dpage/pgadmin4` | `44063` |

Kedua container menggunakan kebijakan restart `unless-stopped`. Logging container pgAdmin dinonaktifkan (`driver: none`).

## Persiapan

Buat file `.env` di folder `docker_postgres` dengan kredensial PostgreSQL:

```env
POSTGRES_USER=user
POSTGRES_PASSWORD=password
```

Kedua variabel tersebut harus diisi. Kredensial pgAdmin dapat diatur melalui `PGADMIN_DEFAULT_EMAIL` dan `PGADMIN_DEFAULT_PASSWORD`. Jika tidak diatur, nilainya adalah:

```env
PGADMIN_DEFAULT_EMAIL=pgadmin4@pgadmin.org
PGADMIN_DEFAULT_PASSWORD=admin
```

Ganti kredensial bawaan pgAdmin sebelum digunakan.

## Menjalankan

Dari folder `docker_postgres`, jalankan:

```sh
docker compose up -d
```

Perintah untuk memulai, restart, dan stop container:

```sh
docker compose start
docker compose 
docker compose stop
```

## Akses

- **pgAdmin:** <http://localhost:44063>. Gunakan email dan password pgAdmin yang sudah ditentukan.
- **PostgreSQL dari host:** host `localhost`, port `22063`, serta username dan password dari `.env`.
- **PostgreSQL dari pgAdmin:** tambahkan server dengan hostname `postgres` dan port `5432`; gunakan kredensial PostgreSQL dari `.env`.

## Penyimpanan data

Volume Docker `postgres15` menyimpan data PostgreSQL di `/data/postgres`, dan volume `pgadmin` menyimpan data pgAdmin di `/var/lib/pgadmin`. `docker compose down` mempertahankan volume tersebut. Untuk menghapus container sekaligus seluruh data pada volume, jalankan `docker compose down -v`.
