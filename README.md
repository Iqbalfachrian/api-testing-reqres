# ReqRes API Testing Sample

Mini-project portfolio QA untuk Iqbal yang mendemonstrasikan functional REST API testing menggunakan Postman dan [ReqRes](https://reqres.in/).

Project ini diposisikan sebagai supporting portfolio project: cukup untuk menunjukkan cara menyiapkan request, membaca HTTP status code, membuat assertion, dan menguji positive/negative scenario. Ini bukan framework automation penuh, performance test, atau security test.

## Objective

- Menguji endpoint REST API dengan method GET, POST, PUT, PATCH, dan DELETE.
- Memvalidasi HTTP status code dan bagian penting dari response body.
- Menunjukkan positive scenario dan negative/validation scenario.
- Menambahkan response-time check sederhana di Postman.
- Menyimpan credential di environment placeholder, bukan di collection atau source code.

## Scope dan coverage

Collection berisi 11 scenario:

| Area | Scenario | Status yang diharapkan |
| --- | --- | ---: |
| Users | List users | 200 |
| Users | Get single user | 200 |
| Users | Get missing user | 404 |
| CRUD | Create user | 201 |
| CRUD | Update dengan PUT | 200 |
| CRUD | Partial update dengan PATCH | 200 |
| CRUD | Delete user | 204 |
| Authentication | Register berhasil | 200 |
| Authentication | Register tanpa password | 400 |
| Authentication | Login berhasil | 200 |
| Authentication | Login tanpa password | 400 |

Detail tujuan dan assertion tersedia di [`docs/test-scenarios.md`](docs/test-scenarios.md).

## Struktur project

```text
api-testing-reqres/
├── postman/
│   ├── ReqRes-API-Testing.postman_collection.json
│   └── ReqRes.postman_environment.json
├── docs/
│   └── test-scenarios.md
└── README.md
```

## Cara menjalankan di Postman

1. Buat atau ambil API key dari dashboard ReqRes.
2. Import dua file JSON di folder `postman/`.
3. Pilih environment `ReqRes`.
4. Buka variable `api_key` dan ganti `PASTE_YOUR_REQRES_API_KEY_HERE` dengan API key milik sendiri.
5. Jalankan satu request terlebih dahulu, misalnya `List users - 200`.
6. Setelah response masuk, buka tab **Test Results** untuk membaca assertion.
7. Jalankan collection dengan Collection Runner jika sudah memahami tiap request.

Dokumentasi current ReqRes menyatakan bahwa API request membutuhkan header `x-api-key`. API key sengaja tidak disertakan di repository ini. Jangan commit API key pribadi ke GitHub.

## Apa yang didemonstrasikan

- Penyusunan request berdasarkan method dan endpoint.
- Environment variable untuk `base_url`, API key, id user, dan threshold response time.
- Assertion status code: 200, 201, 204, 400, dan 404.
- Assertion response body: array, object, field bisnis, token, error, dan metadata timestamp.
- Pengambilan nilai dari response ke environment variable melalui `pm.environment.set`.
- Pemisahan positive scenario dan negative scenario.
- Basic response-time check dengan threshold yang dapat dikonfigurasi.

## Batasan dan interpretasi hasil

- Test ini menggunakan service pihak ketiga, sehingga availability, rate limit, network, dan policy ReqRes dapat memengaruhi hasil.
- Threshold `2000 ms` hanya contoh untuk latihan, bukan SLA ReqRes.
- Collection ini tidak mengklaim telah menguji seluruh API, security, load/performance, data persistence, atau production readiness.
- Jika expected status gagal, baca response aktual dan error message. Jangan sekadar mengganti assertion agar test pass.

## Sumber resmi

- [ReqRes API docs](https://reqres.in/docs)
- [ReqRes OpenAPI specification](https://reqres.in/openapi.json)
- [ReqRes API testing with Postman guide](https://reqres.in/blog/api-testing-with-postman)

Dokumentasi dan endpoint dicek pada 26 September 2026. Karena service eksternal dapat berubah, cek kembali dokumentasi ReqRes sebelum menjalankan atau mempublikasikan ulang sample ini.
