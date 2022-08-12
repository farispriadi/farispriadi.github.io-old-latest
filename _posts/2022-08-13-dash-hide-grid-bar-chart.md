---
layout: post
title:  "Menyembunyikan grid Bar Chart"
author: faris
categories: [ dash, plotly, bar chart, tutorial ]
image: https://images.pexels.com/photos/164686/pexels-photo-164686.jpeg
---
Secara default untuk membuat Bar Chart pada Dash Plotly grid pada tampilan grafik akan muncul. Pada post kali ini akan kita sembunyikan grid pada Bar Chart.


## Membuat Bar Chart

Kita akan membuat Bar Chart menggunakan kode dari [Membuat Bar Chart dengan Dash Plotly](https://farispriadi.github.io/dash-simple-bar-chart/).


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
					html.H2("Bar Chart Sederhana dengan Dash Plotly")
				]),
				html.Div([
					# Div untuk Bar Chart
					dcc.Graph( figure =
						go.Figure(
							go.Bar(x=['Jawa Barat','Jawa Tengah','Jawa Timur'], y=[27,35,38])
						)


					)
				]),
			])

if __name__ == '__main__':
	app.run_server()


```

## Menghilangkan Grid
Grid pada bar chart hanya muncul pada subu y saja, sehingga cukup menyembunyikan garis yang muncul dari yaxis. Dengan membuat objek dari*go.Layout* dan diisi dengan dictionary dengan *key* *yaxis: {'showgrid': False}*. Sehingga kode akan menjadi sebagai berikut.

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
					html.H2("Bar Chart Sederhana dengan Dash Plotly")
				]),
				html.Div([
					# Div untuk Bar Chart
					dcc.Graph( figure =
						go.Figure(
							go.Bar(x=['Jawa Barat','Jawa Tengah','Jawa Timur'], y=[27,35,38]),
							go.Layout(yaxis={'showgrid': False})
						)


					)
				]),
			])

if __name__ == '__main__':
	app.run_server()
```
## Menjalankan Kode

Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *no_grid_bar_chart.py*) lalu kita jalankan dengan perintah.

```
$ python no_grid_bar_chart.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.
![Tampilan]({{ site.baseurl }}/assets/images/hide_grid_bar_chart.png)