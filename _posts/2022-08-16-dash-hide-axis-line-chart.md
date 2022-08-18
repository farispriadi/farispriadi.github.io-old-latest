---
layout: post
title:  "Menyembunyikan x axis atau y axis pada Line Chart"
author: faris
categories: [ dash, plotly, line chart, tutorial ]

image: https://images.pexels.com/photos/590011/pexels-photo-590011.jpeg
---
Pada post kali ini kita akan mencoba menghilangkan garis y axis dan menggantinya dengan memberikan text label.

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
					html.H2("Line Chart Dengan Text Label")
				]),
				html.Div([
					# Div untuk Line Chart
					dcc.Graph(figure=
							go.Figure(
								go.Scatter(
								x = [1,2,3,4],
								y = [1,4,9,16],
								mode='lines+markers+text',
								text=['1^2','2^2','3^2','4^2'],
								textposition = 'top right',
							),
							go.Layout(
								xaxis={'showgrid':False},
								yaxis={'showgrid':False}
							)
						)
					)
				]),
			])

if __name__ == '__main__':
	app.run_server()

```


## Menulis blok kode

Selanjutnya kita akan menyembunyikan garis Y axis.

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
					html.H2("Menyembunyikan Y Axis Pada Line Chart")
				]),
				html.Div([
					# Div untuk Line Chart
					dcc.Graph(figure=
							go.Figure(
								go.Scatter(
								x = [1,2,3,4],
								y = [1,4,9,16],
								mode='lines+markers+text',
								text=[1,4,9,16],
								textposition = 'top right',
							),
							go.Layout(
								xaxis={'showgrid':False},
								yaxis={'showgrid':False, 'visible': False, 'showticklabels': False}
							)
						)
					)
				]),
			])

if __name__ == '__main__':
	app.run_server()

```

Pada kode di atas kita mengganti Text Label dari ['1^2','2^2','3^2','4^2'] menjadi nilai dari Y yaitu [1,4,9,16]. Untuk menyembunyikan garis sumbu y pada parameter 'yaxis' ditambahkan *key* 'visible' dan 'showticklabels' yang keduanya bernilai False. Jika diperlukan untuk menyembunyikan sumbu x, kita juga bisa melakukann hal yang sama pada parameter 'xaxis'.

## Menjalankan Kode


Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *line_chart_hide_axis.py*) lalu kita jalankan dengan perintah.

```
$ python line_chart_hide_axis.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.

![Tampilan]({{ site.baseurl }}/assets/images/line_chart_hide_axis.png)
