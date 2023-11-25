# Data-Preprocessing
## Label Encoding:

1. **Tujuan:**
   - Label Encoding digunakan untuk mengubah nilai kategori menjadi nilai numerik.
   - Berguna saat terdapat urutan atau tingkatan yang signifikan antara kategori.

2. **Contoh Penggunaan:**
   - Misalkan kita memiliki kategori "rendah," "sedang," dan "tinggi" yang memiliki urutan, seperti pada variabel tingkat pendapatan.

3. **Implementasi:**
   - Menggunakan `LabelEncoder` dari Sklearn.
   - Proses ini memberikan nilai numerik secara langsung sesuai dengan urutan kategori.

    ```python
    from sklearn.preprocessing import LabelEncoder

    le = LabelEncoder()
    df['kolom_kategorikal'] = le.fit_transform(df['kolom_kategorikal'])
    ```

4. **Output:**
   - Kolom kategorikal menjadi nilai numerik sesuai urutan kategori.
   ```plaintext
   Kolom_Kategorikal
   0
   1
   2
   0
   1
   ```

5. **Kelebihan dan Keterbatasan:**
   - Kelebihan: Mudah diimplementasikan, efisien untuk data dengan urutan.
   - Keterbatasan: Tidak cocok untuk data tanpa urutan; model bisa salah menginterpretasikan hubungan ordinal sebagai hubungan interval.

## One-Hot Encoding (OHE):

1. **Tujuan:**
   - One-Hot Encoding digunakan untuk mengatasi ketidakberaturan dan mengubah setiap kategori menjadi kolom biner terpisah.

2. **Contoh Penggunaan:**
   - Cocok untuk data di mana tidak ada urutan yang signifikan antara kategori, seperti jenis kelamin atau warna.

3. **Implementasi:**
   - Menggunakan `OneHotEncoder` dari Sklearn atau fungsi `get_dummies` dari Pandas.
   - Setiap kategori diubah menjadi kolom baru, dan keberadaan kategori ditandai dengan 1.

    ```python
    # Menggunakan Sklearn OneHotEncoder
    from sklearn.preprocessing import OneHotEncoder
    from sklearn.compose import ColumnTransformer

    ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(), ['kolom_kategorikal'])], remainder='passthrough')
    df = pd.DataFrame(ct.fit_transform(df))

    # Atau menggunakan Pandas get_dummies
    df = pd.get_dummies(df, columns=['kolom_kategorikal'])
    ```

4. **Output:**
   - Setiap kategori menjadi kolom baru dengan nilai 0 atau 1.
   ```plaintext
   Kolom_Kategorikal_0 Kolom_Kategorikal_1 Kolom_Kategorikal_2
   1                   0                   0
   0                   1                   0
   0                   0                   1
   1                   0                   0
   0                   1                   0
   ```

5. **Kelebihan dan Keterbatasan:**
   - Kelebihan: Cocok untuk data tanpa urutan, menghindari interpretasi ordinal yang salah.
   - Keterbatasan: Menambah dimensi data (khususnya jika terdapat banyak kategori) dan bisa menjadi masalah jika terdapat kategori baru dalam data uji yang tidak ada dalam data latih.

Pilihan antara Label Encoding dan One-Hot Encoding tergantung pada sifat data kategorikal Anda dan persyaratan model pembelajaran mesin yang Anda terapkan.
