---
layout: post
title:  "Mengurutkan Nilai pada Dash Data Table"
author: faris
categories: [ dash, plotly, table, tutorial ]
image: https://images.pexels.com/photos/164686/pexels-photo-164686.jpeg
---
Kita sering menemukan tabel dan dalam membaca tabel tentu saja mau tidak mau kita akan mulai dari kiri atas menuju ke kanan atas untuk membaca semua kolom, kemudian secara zigzag pindah ke kiri di bawah menuju kanan bawah. Namun Setelah kita menemukan kolom yang kita lebih berikan perhatian, kita cenderung membaca dari atas ke bawah. Untuk memudahkan dalam pembacaan data, akan lebih mudah kiranya jika kita dapat mengurutkan sebuah kolom baik urut secara *ascending* maupun *descending*.


## Membuat Table

Dengan Dash Datatable memungkinkan sebuah kolom dari sebuah table dapat diurutkan. Untuk membuat sebuah tabel dapat diurutkan kita akan memerlukan parameter *sort_action='native'* pada saat membuat objek DataTable. Kita akan menggunakan kode dari [Membuat Table dengan Dash Plotly](https://farispriadi.github.io/dash-data-table/)


```
import dash
from dash import dash_table
from dash import html
import pandas as pd

app = dash.Dash(__name__)

df = pd.DataFrame("http://data.bandung.go.id/dataset/fb75420f-05b5-4f50-997a-b2097a932270/resource/37bbbf28-0bec-4103-b3d2-dd148d368efa/download/data-laporan-iklim-1976-2017.csv")

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

## Menambahkan Fitur Pengurutan (Sorting)

Kita perlu menambahkan *sort_action='native'* pada saat instantiasi DataTable, sehingga kode akan menjadi sebagai berikut. selain itu kita akan menambahkan *keyword argument* yaitu *data* dan *columns*.

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
					html.H2("Tabel Dengan  Dash Plotly")
				]),
				html.Div([
					# Div untuk table
					dash_table.DataTable(
						data = df.to_dict('records'), 
						columns=[ {'name': i, 'id': i} for i in df.columns],
						sort_action='native',
					)
				]),
			])

if __name__ == "__main__":
	app.run_server()

```
Dari kode di atas kita sudah bisa melakukan pengurutan pada sebuah tabel. Namun jika kita memerlukan fitur agar pengurutan bisa dilakukan pada multi kolom, perlu ada tambahan argumen lagi yaitu *sort_mode='multi'*. 


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
					html.H2("Tabel Dengan  Dash Plotly")
				]),
				html.Div([
					# Div untuk table
					dash_table.DataTable(
						data = df.to_dict('records'), 
						columns=[ {'name': i, 'id': i} for i in df.columns],
						sort_action='native',
						sort_mode='multi',
					)
				]),
			])

if __name__ == "__main__":
	app.run_server()

```

Dengan menambahkan fitur *sort_mode='multi'* memungkinkan tabel dapat diurutkan berdasarkan 2 atau lebih kolom.


## Menjalankan Kode

Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *sortable_table.py*) lalu kita jalankan dengan perintah.

```
$ python sortable_table.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.
