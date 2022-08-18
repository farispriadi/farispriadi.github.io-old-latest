---
layout: post
title:  "Menambahkan Text Label pada Bar Chart dengan Dash Plotly."
author: faris
categories: [ dash, plotly, bar chart, tutorial ]
image: https://images.pexels.com/photos/590020/pexels-photo-590020.jpeg
---
Memberikan Text Label pada Bar Chart memudahkan pengguna untuk melihat nilai pada sumbu y tanpa harus menurutkannya ke sumbu y sendiri, artinya dapat mengurangi energi yang dikeluarkan oleh pengguna dalam melihat sebuah grafik. Pada post kali ini kita akan membahas mengenai panambahan Text Label pada Bar Chart.

## Membuat Bar Chart

Kita akan menggunakan contoh pada post [Menyembunyikan grid Bar Chart](https://farispriadi.github.io/dash-hide-grid-bar-chart/).

```
import dash
from dash import html
from dash import dcc
from plotly import graph_objects as go

app = dash.Dash(__name__)

app.layout = html.Div([
				# Div utama
				html.Div([
					# Div untuk Judul
					html.H2("Bar Chart dengan Text Label")
				]),
				html.Div([
					# Div untuk Bar Chart
					dcc.Graph( figure =
						go.Figure(
							go.Bar(
								x=['Jawa Barat','Jawa Tengah','Jawa Timur'], 
								y=[27,35,38],
							)
						)


					)
				]),
			])

if __name__ == '__main__':
	app.run_server()

```

## Menulis Kode 

```
import dash
from dash import html
from dash import dcc
from plotly import graph_objects as go

app = dash.Dash(__name__)

app.layout = html.Div([
				# Div utama
				html.Div([
					# Div untuk Judul
					html.H2("Bar Chart dengan Text Label")
				]),
				html.Div([
					# Div untuk Bar Chart
					dcc.Graph( figure =
						go.Figure(
							go.Bar(
								x=['Jawa Barat','Jawa Tengah','Jawa Timur'], 
								y=[27,35,38],
								text=[27,35,38],
								textposition = 'inside',
								textfont=dict(size=16)
							),
							go.Layout(yaxis={'showgrid': False})
						)


					)
				]),
			])

if __name__ == '__main__':
	app.run_server()

```

Parameter *text* ditambahkan untuk menampilkan text label. Parameter *textposition* digunakan untuk menentukan posisi text label pada diagram batang, dan *textfont* berisi *dict* untuk konfigurasi font dengan yang berukuran 16 pixel.  

## Menjalankan Kode



Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *bar_chart_with_text_label.py*) lalu kita jalankan dengan perintah.

```
$ python bar_chart_with_text_label
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.

![Tampilan]({{ site.baseurl }}/assets/images/bar_chart_with_text_label.png)