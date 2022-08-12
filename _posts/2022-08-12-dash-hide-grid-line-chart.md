---
layout: post
title:  "Menyembunyikan Grid pada Line Chart"
author: faris
categories: [ dash, plotly, line chart, tutorial ]
image: https://images.pexels.com/photos/164686/pexels-photo-164686.jpeg
---
Terkdang untuk membuat sebuah garis tren dalam Line Chart kita memerlukan untuk membuat semua yang item mengganggu untuk dihilangkan. Grid pada Line Chart termasuk item yang selalu muncul dibelakang garis. Grid dapat membuat sebuah Line Chart bertambah ruwet ketika dibaca. Kita dapat menghilangkannya jika memang diperlukan agar sebuah grafik dapat lebih mudah dilihat trennya.


## Membuat Line Chart

Kita akan membuat Line Chart menggunakan kode dari [Membuat Line Chart dengan Dash Plotl](https://farispriadi.github.io/dash-simple-line-chart/).


```
import dash
from dash import html
from dash import dcc

app = dash.Dash(__name__)

app.layout = html.Div([
				# Div utama
				html.Div([
					# Div untuk Judul
					html.H2("Line Chart Sederhana dengan Dash Plotly")
				]),
				html.Div([
					# Div untuk Line Chart
					dcc.Graph( figure =
						{
							'data' : [{
								'x' : [1,2,3,4,5,6,7,8,9],
								'y' : [1,4,9,16,25,36,49,64,81],
								'mode': 'lines',

							}],
							'layout' : {
								'title' : 'Pangkat Kuadrat',
							}
						}


					)
				]),
			])

if __name__ == '__main__':
	app.run_server()

```

## Menghilangkan Grid
Untuk menghilangkan grid atau garis yang melintang baik dari sumbu x maupun y cukup dengan menambahkan *key* *xaxis: {'showgrid': False}* dan *yaxis: {'showgrid': False}* pada dictionar layout. Sehingga kode akan menjadi sebagai berikut.

```
import dash
from dash import html
from dash import dcc

app = dash.Dash(__name__)

app.layout = html.Div([
				# Div utama
				html.Div([
					# Div untuk Judul
					html.H2("Line Chart Sederhana dengan Dash Plotly")
				]),
				html.Div([
					# Div untuk Line Chart
					dcc.Graph( figure =
						{
							'data' : [{
								'x' : [1,2,3,4,5,6,7,8,9],
								'y' : [1,4,9,16,25,36,49,64,81],
								'mode': 'lines',

							}],
							'layout' : {
								'title' : 'Pangkat Kuadrat',
								'xaxis' : {'showgrid': False},
								'yaxis' : {'showgrid': False}
							}
						}


					)
				]),
			])

if __name__ == '__main__':
	app.run_server()
```
## Menjalankan Kode

Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *no_grid_line_chart.py*) lalu kita jalankan dengan perintah.

```
$ python no_grid_line_chart.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.
![Tampilan]({{ site.baseurl }}/assets/images/hide_grid_line_chart.png)