---
layout: post
title:  "Membuat Table dengan Dash Plotly"
author: faris
categories: [ dash, plotly, table, tutorial ]
image: https://images.pexels.com/photos/164686/pexels-photo-164686.jpeg
tags: [featured]
---
Tabel digunakan untuk menampilkan data dalam bentuk baris dan kolom. Tabel lebih mudah digunakan untuk menyajikan komparasi data yang mempunyai perbedaan unit. Dengan menggunakan Dash Datatable kita akan membuat tampilan tabel sederhana.

## Import modul yang diperlukan

```
import dash
from dash import dash_table
from dash import html
import pandas as pd


```

*import dash* digunakan untuk mengimpor modul dash. untuk membuat table kita perlu mengimpor *dash_table* dari modul *dash*. *from dash import html* digunakan untuk mengimpor html dash atau *dash html components*, komponen ini memungkinkan kita memasukkan komponen HTML dengan menggunakan sintaks python. Kita perlu membuat dataframe dengan membaca sebuah csv file dari url, sehingga untuk mebgimpor pandas kita perlu menuliskan *import pandas as pd*.

## Membuat Layout

```
import dash
from dash import dash_table
from dash import html
import pandas as pd

app = dash.Dash(__name__)

app.layout = html.Div([
				html.Div([
					# Div untuk judul
				]),
				html.Div([
					# Div untuk table
				]),
			])


```
*app = dash.Dash(\_\_name\_\_)* kode ini adalah langkah awal kita untuk membuat objek dash yang disimpan dalam variable *app*. Selanjutnya *app.layout*, kita akan meng-assign atau memasukkan layout kita ke dalam atribut layout yang berada di dalam *app*. Layout tersebut akan kita buat dengan satu *Div* utama dan di dalamnya terdapat dua *Div* anakan. Dimana *Div* pertama untuk meletakkan judul dan *Div* kedua untuk meletakkan tabel. Tanda *#* merupakan *comment* yang digunakan sebagai keterangan saja.


## Menuliskan konten

Disini kita akan mengisi bagian Div yang sudah kita buat sebelumnya dengan judul dan tabel.

```
import dash
from dash import dash_table
from dash import html
import pandas as pd

app = dash.Dash(__name__)

df = pd.read_csv("http://data.bandung.go.id/dataset/fb75420f-05b5-4f50-997a-b2097a932270/resource/37bbbf28-0bec-4103-b3d2-dd148d368efa/download/data-laporan-iklim-1976-2017.csv")

app.layout = html.Div([
				html.Div([
					# Div untuk judul
					html.H2("Tabel Sederhana Dash Plotly")
				]),
				html.Div([
					# Div untuk table
					dash_table.DataTable(df.to_dict('records'), [ {'name': i, 'id': i} for i in df.columns])
				]),
			])

if __name__ == "__main__":
	app.run_server()


```

Kita perlu membuat sebuah Dataframe yang disimpan dalam variable *df*. Dataframe tersebut dibuat dengan membaca file csv dari url yang kami ambil dari Bandung Open Data dengan judul **Tahun 2017 - Data Laporan Iklim Kota Bandung**. Untuk membuat judul dengan ukuran heading 2 perlu menggunakan kode *html.H2*. Sedangkan tabel dibuat dengan meninstantiasi objek dari *dash_table.DataTable*, dimana argumen pertama diisi dengan *dictionary* yang merupakan konversi dari Dataframe dan argumen kedua adalah nama sebuah *list of dictionary* untuk membuat label kolom tabel.

## Menjalankan Kode

Selanjutnya kita bisa simpan dengan nama *simple_table.py* , dan menjalankan kode diatas dengan perintah seperti di bawah ini.

```
$ python simple_table.py

Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```

Sekarang anda dapat membuka browser dan mengakses aplikasi dash dengan alamat url *http://127.0.0.1:8050* 

![Tampilan]({{ site.baseurl }}/assets/images/simple_table.png)