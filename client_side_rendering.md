# Client Side Rendering 

## Apa itu Client Side Rendering?
Client-Side Rendering (CSR) adalah teknik rendering di mana halaman web di-render sepenuhnya di sisi klien (browser) setelah halaman dimuat. JavaScript mengambil alih proses rendering dan interaksi pengguna. Next.js, sebagai framework React yang populer, mendukung CSR secara penuh dan bahkan menggabungkannya dengan teknik rendering lainnya seperti Server-Side Rendering (SSR) dan Static Site Generation (SSG) untuk memberikan fleksibilitas yang tinggi dalam membangun aplikasi web.

## Kapan Menggunakan Client Side Rendering?
CSR cocok digunakan dalam situasi berikut:

- **Interaksi Dinamis**: Aplikasi dengan interaksi pengguna yang intensif setelah halaman dimuat.
- **Data yang Berubah-ubah**: Ketika data perlu diperbarui secara real-time atau sering berubah.
- **Pengalaman Pengguna yang Kaya**: Aplikasi yang membutuhkan rendering di sisi klien untuk fitur-fitur seperti animasi kompleks atau manipulasi DOM.

Namun, perlu diperhatikan bahwa CSR mungkin memiliki waktu muat awal yang lebih lambat dibandingkan SSR atau SSG karena browser harus mengeksekusi JavaScript sebelum menampilkan konten.

## Implementasi CSR
Di Next.js, ada dua cara Anda dapat mengimplementasikan rendering sisi klien:
- Menggunakan hook React useEffect()di dalam halaman Anda, bukan metode rendering sisi server ( getStaticPropsdan getServerSideProps).
- Menggunakan pustaka pengambilan data seperti SWRatau Kueri TanStackuntuk mengambil data pada klien (disarankan).

Berikut contoh penggunaan ```useEffect()```di dalam halaman Next.js:
```js
import React, { useState, useEffect } from 'react'
 
export function Page() {
  const [data, setData] = useState(null)
 
  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch('https://api.example.com/data')
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`)
      }
      const result = await response.json()
      setData(result)
    }
 
    fetchData().catch((e) => {
      // handle the error as needed
      console.error('An error occurred while fetching the data: ', e)
    })
  }, [])
 
  return <p>{data ? `Your data: ${data}` : 'Loading...'}</p>
}
```
Dalam contoh di atas, komponen dimulai dengan merender ```Loading....``` Kemudian, setelah data diambil, komponen akan merender ulang dan menampilkan data.

### Kelebihan dan Kekurangan CSR

- **Kelebihan:**
    - Interaktif
    - Pengalaman pengguna yang baik
    - Pengembangan yang mudah
- **Kekurangan:**
    - SEO kurang baik (halaman tidak di-index oleh mesin pencari secara langsung)
    - Waktu loading awal bisa lebih lama