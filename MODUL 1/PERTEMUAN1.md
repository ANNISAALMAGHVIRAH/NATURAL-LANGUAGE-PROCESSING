## LAPORAN PRAKTIKUM
## NATURAL LANGUAGE PROCESSOR




Annisa Almaghvirah
240306037


## Modul 	Modul 1 - Fundamental dan Text Processing
## Topik	Eksplorasi Corpus

	Tujuan 
Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
	Membaca Dataset CSV
	Memahami Struktur Corpus
	Mengetahui Jumlah Dokumen
	Mengetahui Jumlah Kolom
	Mengetahui Jumlah Data
	Mengetahui Distribusi Data
	Menghitung Jumlah Kalimat
	Menghitung Jumlah Kata
	Melakukan Eksplorasi Awal Dataset

	Requiretment
	Sistem Operasi yang digunakan : Windows 11 Home Single Language 64-
bit (10.0, Build 26100)
	Browser	: Google Chrome Version 130.0.6723.117 (Official Build) (64-bit)
	Tools yang digunakan	: Visual Studio Code

	Konsep Dasar
	Pengertian NLP
Natural Language Processing (NLP) adalah cabang kecerdasan buatan yang memungkinkan komputer untuk memahami, mengolah, dan menghasilkan bahasa alami (bahasa manusia).
Contoh aplikasi NLP:
	Mesin penerjemah (Google Translate)
	Asisten virtual (Siri, Google Assistant)
	Deteksi spam email
	Analisis sentimen ulasan produk
	Chatbot layanan pelanggan
	Ringkasan dokumen otomatis
	NLP Klasik vs Modern
Era	Pendekatan	Contoh
Klasik	Berbasis aturan (rule-based)	Regex, grammar rules
Statistik	 Probabilitas & frekuensi	N-gram, Naive Bayes
Machine Learning 	Representasi fitur manual	SVM, Decision Tree
Deep Learning	Representasi otomatis	RNN, LSTM
Modern	Pretrained Transformer	BERT, GPT, IndoBERT

	Level Pemrosesan Bahasa
NLP memproses bahasa pada berbagai level:
Lexical → Kata dan morfologi
Syntactic → Struktur kalimat (grammar)
Semantic → Makna kata dan kalimat
Discourse → Hubungan antar kalimat
Pragmatic → Konteks dan tujuan komunikasi
	Apa Itu Corpus?
Dalam NLP, corpus adalah kumpulan data bahasa yang digunakan untuk analisis atau pengembangan sistem NLP.
Dokumen 1
Dokumen 2
Dokumen 3
...
Dokumen N
Sebuah corpus dapat berupa:
	berita;
	review produk;
	komentar media sosial;
	tweet;
	dokumen akademik;
	percakapan;
	pengaduan masyarakat.

	Dataset CSV
Dataset yang digunakan mahasiswa minimal memiliki satu kolom teks.
Contoh:
id	text	label
1	Pelayanan hotel sangat bagus	Positif
2	Kamar hotel sangat kotor	Negatif
3	Lokasi hotel cukup strategis	positif 

Nama kolom setiap dataset dapat berbeda. Mahasiswa harus mengidentifikasi sendiri kolom yang berisi teks.

	Implementasi 
	Membuat Folder Project
 
Folder paling luar (root) adalah Modul-1, yang di dalamnya langsung menampung folder lingkungan virtual .venv, sub-folder pertemuan-01, file dataset review_gopay_newest_sort.csv, dan file Jupyter Notebook test_environment.ipynb. Sementara itu, di dalam sub-folder pertemuan-01 terdapat satu file tersendiri, yaitu eksplorasi_corpus.ipynb.
	Membuat Virtual Environment
Jalankan:
python -m venv .venv
Aktifkan virtual environment:
.venv\Scripts\activate
Jika berhasil, terminal akan menampilkan:
(.venv)
Contoh:
(.venv) C:\Users\Nama\NLP\modul-1>

Perintah tersebut diawali dengan membuat virtual environment baru bernama .venv melalui perintah python -m venv .venv. Setelah itu, kebijakan eksekusi PowerShell diizinkan untuk sesi aktif (Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass) agar script aktivasi & .\.venv\Scripts\Activate.ps1 bisa dijalankan hingga muncul tanda (.venv). Terakhir, dilakukan dua tahap verifikasi untuk memastikan lingkungan virtual siap digunakan: mengecek versi Python yang terinstal (Python 3.13.15) dan memvalidasi jalur eksekusi Python yang sudah mengarah langsung ke folder virtual tersebut (D:\NLP\.venv\Scripts\python.exe).
	Install Library
pip install pandas numpy matplotlib seaborn nltk spacy Sastrawi scikit-learn jupyter

Perintah pip install dijalankan di dalam lingkungan virtual .venv untuk menginstal beberapa library analisis data dan NLP sekaligus (pandas, numpy, matplotlib, seaborn, nltk, spacy, Sastrawi, scikit-learn, dan jupyter). Hasilnya menunjukkan bahwa sebagian besar paket (seperti pandas, numpy, matplotlib, nltk, spacy, Sastrawi, dan jupyter) sudah terinstal sebelumnya (Requirement already satisfied). Sistem hanya mengunduh paket yang belum ada atau perlu diperbarui, yaitu seaborn dan scikit-learn beserta dependensinya.
	Memeriksa Instalasi
# Import Library
import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

import seaborn as sns

import nltk

#  Memeriksa Instalasi
nltk.download("punkt")

nltk.download("punkt_tab")


# Load Dataset
data = pd.read_csv('../review_gopay_newest_sort.csv')

print("Jumlah data:", len(data))

# Melihat Data Awal
# 10 data pertama
print(data.head(5))
# 10 data terakhir
print(data.tail(5))

# Informasi dataset
data.info()

# ukuran dataset
print("Ukuran dataset:", data.shape)

# melihat nama kolom
print("Nama kolom:", data.columns)

# melihat jumlah dokumen dalam dataset
jumlah_dokumen = len(data)

print("Jumlah dokumen:", jumlah_dokumen)

#  Memilih Kolom Teks
text_column = "content"       # ganti nama kolom teks yg sesuai dengan dataset 

texts = data[text_column]

print("kolom content:", texts.head(9))

# melihat contoh teks ulasan
for text in texts.head(10):

    print(text)

    print("-" * 80)

# Memeriksa missing value
print("Jumlah missing value setiap kolom:")

print(data.isnull().sum())

# Menghapus data kosong pada kolom teks
print("Dokumen sebelum menghapus data kosong:", len(data))

data = data.dropna(subset=[text_column]).copy()

print("Dokumen setelah menghapus data kosong:", len(data))

# Memeriksa duplikasi
data.duplicated().sum()

print("Jumlah dokumen duplikat:", data.duplicated().sum())

# Memeriksa duplikasi pada kolom teks
data[text_column].duplicated().sum()

print("Jumlah teks duplikat:",data[text_column].duplicated().sum())

# Menghapus teks duplikat
data = data.drop_duplicates(subset=[text_column])

print("Jumlah dokumen setelah menghapus duplikat:", len(data))

# Menghitung jumlah karakter
data["jumlah_karakter"] = data[text_column].astype(str).apply(len)

print(data["jumlah_karakter"].head(10))

# Menghitung jumlah kata
data["jumlah_kata"] = data[text_column].astype(str).apply(

    lambda x: len(x.split())
)

print(data[[text_column, "jumlah_kata"]].head(10))

# Statistik jumlah kata
print("Statistik Jumlah Kata")

print(data["jumlah_kata"].describe())

print("Rata-rata kata per dokumen:", data["jumlah_kata"].mean())

print("Jumlah kata minimum:", data["jumlah_kata"].min())

print("Jumlah kata maksimum:", data["jumlah_kata"].max())

# Menghitung jumlah kalimat
from nltk.tokenize import sent_tokenize

data["jumlah_kalimat"] = data[text_column].fillna("").astype(str).apply(

    lambda x: len(sent_tokenize(x))

)

# Contoh tokenisasi kalimat
text = "Saya belajar NLP. NLP sangat menarik."

sentences = sent_tokenize(text)

print(sentences)

print("Jumlah kalimat setiap dokumen:")

print(data["jumlah_kalimat"].head(10))

# Statistik corpus
print("Jumlah dokumen :", len(data))

print("Jumlah kata    :", data["jumlah_kata"].sum())

print("Jumlah kalimat :", data["jumlah_kalimat"].sum())

print("Jumlah karakter:", data["jumlah_karakter"].sum())

# Menampilkan dokumen terpendek dan terpanjang
print("\nDokumen terpendek:")

idx_min = data["jumlah_kata"].idxmin()

print("Teks:", data.loc[idx_min, text_column])

print("Jumlah kata:", data.loc[idx_min, "jumlah_kata"])

print("\nDokumen terpanjang:")

idx_max = data["jumlah_kata"].idxmax()

print("Teks:", data.loc[idx_max, text_column])

print("Jumlah kata:", data.loc[idx_max, "jumlah_kata"])

# Visualisasi Distribusi Panjang Dokumen
import pandas as pd

import matplotlib.pyplot as plt

plt.figure(figsize=(10, 5))

plt.hist(data["jumlah_kata"], bins=30)

plt.xlabel("Jumlah Kata")

plt.ylabel("Jumlah Dokumen")

plt.title("Distribusi Panjang Dokumen")

plt.tight_layout()

plt.show()



# tugas analisis
Mahasiswa mampu menjawab:
	Apa nama dataset?
Dataset yang digunakan bernama review_gopay_newest_sort.

	Dataset berasal dari mana?
Dataset berasal dari Kaggle yang dibuat oleh Ardena Afif Pratama.

	Berapa jumlah dokumen?
123253

	Berapa jumlah kolom?
6 kolom 

	Apa nama kolom teks?
Kolom yang digunakan untuk analisis teks adalah content.

	Apakah terdapat missing value?
Berdasarkan pemeriksaan missing value, terdapat 15.928 data kosong pada kolom reviewCreatedVersion. Sementara itu, kolom userName, content, score, thumbsUpCount, dan at tidak memiliki missing value.

	Apakah terdapat data duplikat?
Berdasarkan hasil pemeriksaan, duplikat Keseluruhan Baris (Dokumen): Terdapat 2 data duplikat di mana seluruh isi kolom pada baris tersebut sama persis. Duplikat Isi Teks (Content): Terdapat 44.822 teks duplikat pada kolom ulasan. Hal ini terjadi karena banyak pengguna memberikan ulasan singkat yang sama persis, seperti kata "Mantap", "Bagus", atau "Good". 

	Berapa rata-rata jumlah kata per dokumen?
Rata-rata jumlah kata per dokumen adalah 9.577233491859086 kata.

	Berapa dokumen terpendek?
Dokumen terpendek memiliki 1 kata.

	Berapa dokumen terpanjang?
Dokumen terpanjang memiliki 105 kata.

	Apakah dataset memiliki label?
Dataset tidak memiliki label

	Bagaimana distribusi labelnya?
Karena tidak terdapat kolom label, distribusi label tidak dapat dihitung. Analisis yang dilakukan berfokus pada karakteristik corpus, seperti jumlah dokumen, karakter, kata, kalimat, dan distribusi panjang komentar.

	Apa karakteristik bahasa yang ditemukan?
Berdasarkan eksplorasi dataset ulasan GoPay, karakteristik bahasa yang ditemukan adalah penggunaan bahasa yang relatif beragam, dengan ulasan yang memiliki panjang berbeda-beda. Sebagian besar ulasan cenderung pendek, sedangkan sebagian lainnya lebih panjang dan berisi informasi yang lebih banyak. Selain itu, dataset memiliki rating dari 1 sampai 5, dengan rating 5 sebagai rating yang paling dominan.

# Pertanyaan Diskusi
	Mengapa eksplorasi corpus penting sebelum memulai proses NLP?
Jawaban:
Eksplorasi corpus penting untuk memahami karakteristik dan kondisi dataset sebelum dilakukan pemrosesan teks. Melalui eksplorasi, kita dapat mengetahui jumlah dokumen, jumlah kata, struktur data, data kosong, dan duplikasi. Dengan begitu, kita dapat menentukan langkah preprocessing yang sesuai dan mengurangi kesalahan saat proses NLP.

	Apa perbedaan dokumen, kalimat, kata, dan karakter dalam konteks NLP?
Jawaban:
Dokumen adalah satu unit teks yang dianalisis, misalnya satu ulasan pengguna aplikasi. Kalimat adalah bagian dari dokumen yang berisi satu rangkaian ungkapan, biasanya diakhiri tanda titik, tanda tanya, atau tanda seru. Kata adalah unit bahasa yang terbentuk dari rangkaian huruf dan dipisahkan oleh spasi atau aturan tokenisasi. Sementara itu, karakter adalah setiap simbol dalam teks, termasuk huruf, angka, spasi, dan tanda baca.

	Apakah dataset yang seimbang (balanced) selalu lebih baik?
Jawaban:
Tidak selalu. Dataset yang seimbang berarti jumlah data pada setiap kelas relatif sama. Kondisi ini dapat membantu model mempelajari setiap kelas dengan lebih baik, terutama pada klasifikasi sentimen. Namun, dataset yang tidak seimbang juga dapat mencerminkan kondisi nyata. Oleh karena itu, keseimbangan dataset perlu disesuaikan dengan tujuan penelitian dan jenis masalah yang diselesaikan.

	Mengapa perlu memeriksa missing value dan duplikasi?
Jawaban:
Pemeriksaan missing value diperlukan untuk mengetahui adanya data kosong yang dapat mengganggu proses analisis atau menyebabkan kesalahan saat pemrosesan. Sementara itu, pemeriksaan duplikasi diperlukan untuk mengetahui apakah terdapat data yang tercatat lebih dari satu kali. Data kosong dan duplikat perlu ditangani sesuai kondisi dataset agar hasil analisis lebih akurat dan tidak bias.

	Apa yang dapat disimpulkan dari distribusi panjang dokumen?
Jawaban:
Distribusi panjang dokumen menunjukkan variasi jumlah kata atau karakter dalam setiap dokumen. Dari distribusi tersebut, kita dapat mengetahui apakah sebagian besar dokumen pendek, panjang, atau memiliki panjang yang beragam. Informasi ini dapat digunakan untuk menentukan langkah preprocessing, seperti penanganan dokumen yang terlalu pendek atau panjang, serta membantu menentukan batas panjang teks jika diperlukan dalam pemodelan NLP.

