---
layout: post
title:  "Membuat cell pada Dash Data Table dapat diedit"
author: faris
categories: [ dash, plotly, table, tutorial ]
image: https://images.pexels.com/photos/164686/pexels-photo-164686.jpeg
---
Tabel biasanya digunakan untuk menampilkan data yang mempunyai baris dan kolom. Tabel juga terkadang dibuat tidak hanya untuk menampilkan data namun untuk mengisi data. Kali ini kita akan membuat tabel yang nilainya dapat Anda ubah atau dapat diupdate.


## Membuat Table

Sebagai awalan akan menggunakan kode dari postingan [Membuat Table dengan Dash Plotly](https://farispriadi.github.io/dash-data-table/). 


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

Kode diatas hanya akan menampilkan tabel dengan data namun kita tidak bisa menperbaharui data yang tertera pada setiap *cell*. Kita akan menambahkan *keyword argument* yaitu *data* pada *df.to_dict('records')* dan *columns* pada [ {'name': i, 'id': i} for i in df.columns] . Kita perlu menambahkan *editable=True* pada saat instantiasi DataTable agar fitur untuk mengedit cell dapat aktif. Sehingga kode akan menjadi sebagai berikut.

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
						editable=True,
					)
				]),
			])

if __name__ == "__main__":
	app.run_server()

```
Pada saat kode ini dijalankan kita dapat mengubah nilai dari setiap *cell* yang sudah terisi nilai termasuk mengosongkannya. 


## Menjalankan Kode

Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *editable_table.py*) lalu kita jalankan dengan perintah.

```
$ python editable_table.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.