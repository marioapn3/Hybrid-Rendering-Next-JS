# Server Side Rendering (SSR)

## Apa itu Server Side Rendering (SSR)?

Server Side Rendering (SSR), atau sering disebut Dynamic Rendering, adalah metode rendering di mana halaman web dirender di server setiap kali ada permintaan baru dari pengguna. Ketika pengguna mengunjungi suatu halaman, server langsung menghasilkan HTML untuk halaman tersebut dan mengirimkannya ke browser. Ini berbeda dengan Static Site Generation (SSG), di mana halaman dihasilkan hanya saat build time.

## Bagaimana Cara Kerja Server Side Rendering?

SSR pada aplikasi modern seperti Next.js dan React melibatkan beberapa tahap rendering komponen di sisi server:

1. **Membuat Payload Komponen Server**  
   Rendering dimulai dengan mengubah komponen server menjadi format data khusus yang disebut **React Server Component Payload (RSC Payload)**.

2. **Rendering di Server**  
   Next.js menggunakan RSC Payload bersama instruksi JavaScript dari Komponen Klien untuk menghasilkan HTML di server.

3. **Pengiriman HTML ke Klien**  
   HTML yang dihasilkan dikirim ke klien dan ditampilkan segera sebagai pratayang non-interaktif. Ini memungkinkan halaman termuat lebih cepat untuk pengguna.

4. **Sinkronisasi dan Interaktivitas**  
   RSC Payload membantu menyelaraskan pohon Komponen Klien dan Server. Setelah itu, instruksi JavaScript mengaktifkan Komponen Klien sehingga aplikasi menjadi interaktif dan siap digunakan.

## Keuntungan Server Side Rendering

- **Pengambilan Data**  
  Mempercepat pengambilan data dengan mengurangi waktu dan jumlah permintaan dari client.

- **Keamanan**  
  Data sensitif seperti token dan API key tetap aman di server dan tidak terekspos ke client.

- **Caching**  
  Hasil rendering bisa disimpan (cached) untuk meningkatkan performa pada permintaan berikutnya.

- **Performa**  
  Mengurangi penggunaan JavaScript di sisi client, yang bermanfaat untuk pengguna dengan koneksi internet lambat.

- **Waktu Load Halaman Awal dan First Contentful Paint (FCP)**  
  Pengguna dapat melihat halaman lebih cepat tanpa menunggu seluruh JavaScript dimuat.

- **Search Engine Optimization (SEO)**  
  HTML yang sudah dirender dapat diindeks oleh mesin pencari, mendukung pratayang di media sosial.

- **Streaming**  
  Membuat halaman dapat dimuat lebih cepat karena pengguna bisa melihat konten segera.

## Implementasi Server Side Rendering di Next.js

Jika suatu halaman menggunakan Server Side Rendering, HTML untuk halaman tersebut dihasilkan pada setiap permintaan. Untuk mengaktifkan SSR pada halaman, kita perlu mengekspor fungsi asinkron bernama `getServerSideProps`. Fungsi ini dipanggil oleh server untuk setiap permintaan.

### Contoh Implementasi SSR

Misalnya, untuk merender data yang sering diperbarui dari API eksternal:

```javascript
export default function Page({ data }) {
  // Render data...
}

// Fungsi ini dipanggil pada setiap permintaan
export async function getServerSideProps() {
  // Mengambil data dari API eksternal
  const res = await fetch(`https://.../data`);
  const data = await res.json();

  // Mengirimkan data ke halaman melalui props
  return { props: { data } };
}
