---
layout: post
title:  "Mem-filter nilai dalam sebuah kolom pada Dash Data Table"
author: faris
categories: [ dash, plotly, table, tutorial ]
image: https://images.pexels.com/photos/164686/pexels-photo-164686.jpeg
---
Ketika menemui tabel ada kalanya kita ingin dengan cepat menemukan sebuah nilai yang kita cari dengan cepat. Maka dari itu kita memerlukan fitur filter dalama tabel. Kali ini kita akan menambahkan fitur filter pada Dash Data Table.


## Membuat Table

Dengan Dash Datatable memungkinkan sebuah kolom dari sebuah tabel dapat diurutkan. Untuk membuat sebuah tabel dapat difilter kita akan memerlukan parameter *# filter_action='native'* pada saat membuat objek DataTable. Selanjutnya kita akan mengimplementasikannya dengan menggunakan kode dari [Membuat Table dengan Dash Plotly](https://farispriadi.github.io/dash-data-table/)


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

## Menambahkan Fitur Filter

Pada kode diatas kita tambahkan *keyword argument* untuk *data* dan *columns*.Kita perlu menambahkan *filter_action='native'* untuk mengaktifkan fitur filter pada tiap kolom dalam tabel, sehingga kode akan menjadi sebagai berikut. 

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
						filter_action='native',
					)
				]),
			])

if __name__ == "__main__":
	app.run_server()

```

Dengan menambahkan *sorting* pada laman  [Mengurutkan Nilai pada Dash Data Table](https://farispriadi.github.io/dash-sortable-table/), kita akan dapat mempunyai fitur filter dan sorting.


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
						filter_action='native',
						sort_action='native',
						sort_mode='multi',
					)
				]),
			])

if __name__ == "__main__":
	app.run_server()

```

## Menjalankan Kode

Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *filterable_table.py*) lalu kita jalankan dengan perintah.

```
$ python filterable_table.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.

![Tampilan]({{ site.baseurl }}/assets/images/simple_table_filter.png)
