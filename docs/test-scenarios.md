# ReqRes API Test Scenarios

Dokumen ini menjelaskan tujuan setiap request di collection Postman. Scenario sengaja dibuat kecil agar Iqbal bisa menjalankan, membaca assertion, dan menjelaskan hasilnya saat interview.

## Prasyarat

- Gunakan environment `ReqRes`.
- Isi variable `api_key` dengan API key ReqRes milik sendiri.
- Pilih environment `ReqRes` di Postman sebelum menjalankan request.
- Jalankan collection dari folder `01 - Users and CRUD` lalu `02 - Authentication`.

Menurut [dokumentasi resmi ReqRes](https://reqres.in/docs) yang dicek pada 26 September 2026, request API memakai header `x-api-key`. Collection ini tidak menyimpan API key nyata.

## Coverage matrix

| ID | Scenario | Method | Expected status | Fokus assertion |
| --- | --- | --- | ---: | --- |
| TC-01 | List users | GET | 200 | `data` berupa array, pagination, response time |
| TC-02 | Get single user | GET | 200 | `data.id` sesuai `user_id`, response time |
| TC-03 | Get missing user | GET | 404 | error response, response time |
| TC-04 | Create user | POST | 201 | field request dikembalikan, `id`, `createdAt` |
| TC-05 | Update user with PUT | PUT | 200 | field hasil full update, `updatedAt` |
| TC-06 | Partially update user with PATCH | PATCH | 200 | field yang diubah, `updatedAt` |
| TC-07 | Delete user | DELETE | 204 | response body kosong |
| TC-08 | Register user | POST | 200 | token tersedia |
| TC-09 | Register without password | POST | 400 | error validation |
| TC-10 | Login user | POST | 200 | token tersedia |
| TC-11 | Login without password | POST | 400 | error validation |

## Catatan eksekusi

- TC-04 menyimpan `id` response ke variable `created_user_id` sebagai contoh ekstraksi data response. Scenario lain tetap memakai `user_id=2` supaya dapat dijalankan ulang tanpa bergantung pada urutan request.
- TC-07 memakai status `204 No Content`, sehingga test tidak mencoba parse response sebagai JSON.
- Batas response time default adalah `2000 ms` melalui variable `max_response_time_ms`. Ini adalah threshold praktis untuk sample portfolio, bukan SLA ReqRes.
- Jika request mendapatkan `401` atau `403`, cek API key dan dokumentasi ReqRes terlebih dahulu. Jangan mengubah expected status hanya agar test terlihat hijau.

## Konsep HTTP yang dilatih

- `200 OK`: request berhasil diproses dan response body biasanya berisi hasil operasi.
- `201 Created`: request berhasil dan resource baru dibuat.
- `204 No Content`: operasi berhasil, tetapi server tidak mengembalikan body.
- `400 Bad Request`: input tidak memenuhi kebutuhan endpoint, misalnya password tidak dikirim.
- `404 Not Found`: resource yang diminta tidak ditemukan.

Status code tetap harus dibaca bersama response body, header, dan waktu response. Status `200` saja belum membuktikan bahwa data yang dikembalikan benar.
