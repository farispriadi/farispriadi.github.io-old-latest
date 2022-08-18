---
layout: post
title:  "Menyembunyikan x axis atau y axis pada Bar Chart"
author: faris
categories: [ dash, plotly, bar chart, tutorial ]
image: https://images.pexels.com/photos/590020/pexels-photo-590020.jpeg
---
Kali ini kita akan coba mengimplementasikan Text Label dan menghilangkan sumbu Y.


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
							go.Bar(x=['Jawa Barat','Jawa Tengah','Jawa Timur'], y=[27,35,38],
							text=[27,35,38],
							textposition = 'inside',
							textfont=dict(size=16)
							),
						go.Layout(yaxis={'showgrid': False})
						),
					)
				]),
			])

if __name__ == '__main__':
	app.run_server()


```

## Menghilangkan Sumbu Y


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
					html.H2("Menyembunyikan Y Axis Pada Bar Chart")
				]),
				html.Div([
					# Div untuk Bar Chart
					dcc.Graph( figure =
						go.Figure(
							go.Bar(
								x=['Jawa Barat','Jawa Tengah','Jawa Timur'], y=[27,35,38],
								text=[27,35,38],
								textposition = 'inside',
								textfont=dict(size=16)
							),
						go.Layout(yaxis={'showgrid': False, 'visible': False,'showticklabels': False})	
						),
					)
				]),
			])

if __name__ == '__main__':
	app.run_server()

```

Untuk menyembunyikan sumbu y pada parameter *yaxis* ditambahkan key 'visible' dan 'showticklabels' yang keduanya bernilai False. Jika diperlukan untuk menyembunyikan sumbu x, kita juga bisa melakukann hal yang sama pada parameter *xaxis*.

## Menjalankan Kode

Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *bar_chart_hide_axis.py*) lalu kita jalankan dengan perintah.

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
![Tampilan]({{ site.baseurl }}/assets/images/bar_chart_hide_axis.png)