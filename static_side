# Static Site Generation (SSG)

## Apa itu Static Site Generation?

Static Site Generation (SSG) adalah metode di mana sebuah website dirender menjadi kumpulan *file HTML statis* pada waktu *build* atau *compile*. Hal ini berarti halaman-halaman di dalam situs sudah di-*render* sebelumnya dan siap disajikan kepada pengguna tanpa memerlukan pemrosesan tambahan di server setiap kali halaman diakses.

Berbeda dengan *Server-Side Rendering* (SSR) yang merender halaman saat ada permintaan pengguna, SSG hanya merender halaman sekali, yaitu saat proses build. Ini menjadikan SSG lebih cepat dan efisien.

---

## Kapan Menggunakan Static Site Generation?

SSG direkomendasikan untuk halaman-halaman yang dapat dirender terlebih dahulu sebelum pengguna memintanya. Beberapa jenis halaman yang cocok untuk SSG adalah:

- **Halaman pemasaran (marketing pages)**
- **Artikel blog atau portofolio**
- **Daftar produk e-commerce**
- **Halaman bantuan atau dokumentasi**

Namun, jika halaman membutuhkan data yang sering diperbarui, SSG mungkin kurang cocok. Dalam kasus ini, Anda dapat:

1. Menggunakan SSG dengan **pengambilan data sisi-klien (client-side fetching)** untuk data yang tidak perlu dirender secara statis.
2. Menggunakan **Server-Side Rendering (SSR)** untuk merender halaman setiap kali ada permintaan, meskipun ini lebih lambat dibandingkan SSG.

---

## Implementasi Static Site Generation

### Static Site Generation tanpa Data

Secara default, Next.js akan melakukan pre-render halaman tanpa mengambil data eksternal. Contohnya adalah halaman statis sederhana berikut:

```jsx
function About() {
  return <div>About</div>;
}

export default About;
```
### Static Site Generation dengan Data

Beberapa halaman mungkin memerlukan data eksternal saat pre-rendering, seperti halaman blog yang perlu memuat daftar artikel dari API atau CMS (Content Management System). Ada dua skenario utama:

- Skenario 1 : Konten Halaman Bergantung pada Data Eksternal

Jika konten halaman bergantung pada data eksternal, gunakan fungsi `getStaticProps`. Fungsi ini akan mengambil data selama proses build, dan data tersebut akan dikirim sebagai props ke halaman.

Contoh halaman blog yang memuat daftar postingan dari API eksternal:

```tsx

export default function Blog({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  )
}

// Fungsi ini dipanggil saat build
export async function getStaticProps() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()
 
  return {
    props: {
      posts,
    },
  }
}
```

Pada kode di atas, getStaticProps mengambil data dari API eksternal dan mengirimkannya ke komponen Blog sebagai props saat build.

- Skenario 2 : Path Halaman Bergantung pada Data Eksternal

Jika path (jalur URL) halaman dinamis dan bergantung pada data eksternal, gunakan fungsi `getStaticPaths` bersama `getStaticProps`. Hal ini memungkinkan Next.js untuk mempre-render halaman dengan route dinamis, seperti `/posts/[id]`.

Contohnya, untuk halaman blog yang menampilkan satu postingan berdasarkan `id`:

```tsx 
export default function Post({ post }) {
  return <div>{post.title}</div>
}

// Fungsi ini dipanggil saat build untuk menentukan path yang akan di-render
export async function getStaticPaths() {
  const res = await fetch('https://.../posts')
  const posts = await res.json()
 
  const paths = posts.map((post) => ({
    params: { id: post.id.toString() },
  }))
 
  return { paths, fallback: false }
}

// Fungsi ini juga dipanggil saat build untuk mengambil data postingan berdasarkan id
export async function getStaticProps({ params }) {
  const res = await fetch(`https://.../posts/${params.id}`)
  const post = await res.json()
 
  return { props: { post } }
}
```
Fungsi getStaticPaths di atas menentukan path mana saja yang akan di-render saat build. Sementara getStaticProps mengambil data postingan berdasarkan id dan mengirimkannya sebagai props ke komponen Post.

### Kelebihan dan Kekurangan Static Site Generation?

### Kelebihan

- Server gak terbebani untuk fetch & build
- User bisa cepat nerima halaman webnya
- Gak ada tampilan loading
- Bagus buat SEO

### Kekurangan

- Tidak Cocok untuk data yang sering berubah
- Datanya gak akan update kecuali build ulang
