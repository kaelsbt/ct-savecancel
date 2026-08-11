# CTSaveCancel — Save Cancel / Rollback Exploit untuk "Catch and Tame" (Roblox)

Script riset keamanan game / edukasi exploit Roblox. Rollback murni client-side:
**membatalkan penulisan data**, bukan memutar waktu nyata.

> ⚠️ Melanggar ToS Roblox dan rules game. Gunakan di akun sendiri, sadari
> risiko ban. Untuk tujuan edukasi/riset.

## Cara Kerja

1. Skrip memasang hook di semua jalur save yang bisa dijangkau client:
   - `HttpService` (`PostAsync` / `GetAsync` / `RequestAsync`)
   - `RemoteEvent` / `RemoteFunction` ber-nama "save"
   - fungsi `save` di environment `LocalScript` / `ModuleScript`
2. Setelah hasil gacha jelek, panggil `arm()`.
3. Semua jalur save diblokir + payload rusak dikirim ke remote save agar
   handler server error **sebelum** menulis ke DataStore.
4. Skrip memaksa kick/disconnect sebelum autosave berikutnya.
5. Auto-rejoin ke **server baru** → game membaca DataStore lama →
   mata uang kembali utuh.

## Cara Pakai (Delta — Android)

1. Buka Roblox → masuk ke **Catch and Tame**.
2. Buka Delta executor → **Inject/Attach**.
3. Tempel isi `CTSaveCancel.lua` → **Execute**.
4. Periksa console: pastikan muncul `[CTS] Remote save: ...`
   (artinya jalur save bisa di-intercept). Jika muncul pesan
   "kemungkinan save server-side", trik ini tidak akan bekerja.
5. Main gacha seperti biasa.
6. Jika hasil jelek, ketik di kolom input executor:
   ```lua
   _G.CTSaveCancel:arm("hasil jelek")
