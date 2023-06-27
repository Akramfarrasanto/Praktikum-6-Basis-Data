# Tugas Pertemuan 13 dan 14
## Pertemuan 13
1. Departemen apa saja yang terlibat dalam tiap-tiap project

`select p.nama as perusahaan, d.nama as departemen, pr.nama as project from perusahaan p join departemen d on p.id_p = d.id_p join karyawan k on d.id_dept = k.id_dept join project_detail pd on k.nik = pd.nik join project pr on pd.id_proj = pr.id_proj order by pr.nama;`

<img width="662" alt="1" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/8f4455ae-3226-4973-8532-2e9e41d24014">

2. Jumlah karyawan tiap departemen yang bekerja pada tiap-tiap project

`select p.nama as perusahaan, d.nama as departemen, pr.nama as project, count(distinct k.nik) as jumlah_karyawan from perusahaan p join departemen d on p.id_p = d.id_p join karyawan k on d.id_dept = k.id_dept join project_detail pd on k.nik = pd.nik join project pr on pd.id_proj = pr.id_proj group by p.nama, d.nama, pr.nama order by pr.nama;`

<img width="661" alt="2" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/03db5aab-f488-4274-a25e-bb0514e678fe">

3. Ada berapa project yang sedang dikerjakan oleh departemen RnD? (ket: project berjalan adalah yang statusnya 1)

`select count(distinct pr.id_proj) as jumlah_project from project pr join project_detail pd on pr.id_proj = pd.id_proj join karyawan k on pd.nik = k.nik join departemen d on k.id_dept = d.id_dept where d.nama = 'RnD' and pr.status = 1;`

<img width="658" alt="3" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/a5a0cfd7-ce35-4f99-bc1b-ff34cad7aeef">

4. Berapa banyak project yang sedang dikerjakan oleh Ari?

`select count(distinct pr.id_proj) as jumlah_project from project pr join project_detail pd on pr.id_proj = pd.id_proj where pd.nik = 'N01' and pr.status = 1;` 

<img width="663" alt="4" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/a0d2dc6a-1d08-4d62-97d5-a22978190154">

5. Siapa saja yang mengerjakan projcet B?

`select k.nama from karyawan k join project_detail pd on k.nik = pd.nik join project pr on pd.id_proj = pr.id_proj where pr.nama = 'B';`

<img width="661" alt="5" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/ca6f3747-9e69-4f0a-b2fe-963b532a999f">

## Pertemuan 14 
* Tampilkan data karyawan yang bekerja pada departemen yang sama dengan karyawan yang bernama Dika

`select*from karyawan where id_dept = (select id_dept from karyawan where nama = 'Dika');`

<img width="582" alt="1" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/a0ca6ad9-cbc5-4269-b561-0b31c6cebe54">

* Tampilkan data karyawan yang gajinya lebih besar dari rata-rata gaji semua karyawan. urutkan menurun berdasarkan besaran gaji

`select*from karyawan where gaji_pokok > (select avg(gaji_pokok) from karyawan) order by gaji_pokok descdesc;`

<img width="670" alt="2" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/68118c48-6efd-46d2-8ef8-cfa3741556c0">

* Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di department yang sama dengan karyawan dengan nama yang mengandung huruf 'K'.

`select nik, nama from karyawan where id_dept in (select id_dept from karyawan where nama like '%k%');`

<img width="654" alt="3" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/78c6d7da-d93d-4fba-899b-556c1206300e">

* Tampilkan data karyawan yang bekerja pada departemen yang ada di kantor pusat.

`select*from karyawan join departemen on karyawan.id_dept = departemen.id_dept where departemen.id_p = 'P01';`

<img width="663" alt="4" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/ef51eb69-899c-4d9b-b223-2d589e6dd3d2">

* Tampilkan nik dan nama karyawan untuk semua karyawan yang bekerja di department yang sama dengan karyawan dengan nama yang mengandung huruf 'K' dan yang gajinya lebih besar dari rata-rata gaji semua karyawan

`select distinct k1.nik, k1.nama from karyawan k1 join karyawan k2 on k1.id_dept = k2.id_dept where k1.gaji_pokok > (select avg(gaji_pokok) from karyawan where nama like '%k%');`

<img width="658" alt="5" src="https://github.com/Akramfarrasanto/Praktikum-6-Basis-Data/assets/115552876/2a736d66-715b-4898-b892-501a4cf0d75f">
