---
layout: post
title:  "Menambahkan Text Label pada Line Chart dengan Dash Plotly."
author: faris
categories: [ dash, plotly, line chart, tutorial ]
image: https://images.pexels.com/photos/590011/pexels-photo-590011.jpeg
---
Dalam sebuah grafik garis atau Line Chart kita biasanya memerlukan tambahan text diatas koordinat nilai dari x dan y untuk memudahkan membaca nilai pada titik tersebut. Penambahan text label pada Line Chart akan kita bahas pada post kali ini.

## Import Modul

Berbeda dengan contoh pada post [Membuat Line Chart dengan Dash Plotly](https://farispriadi.github.io/dash-simple-line-chart/), kita akan membuat objek grafik garis tersebut dengan menggunakan modul *graph_objects*

```
import dash
from dash import html
from dash import dcc
from plotly import graph_objects as go

```

impor *graph_objects* dari modul *plotly*, kemudian akses *graph_objects* tersebut dengan menggunakan alias *go*.


## Menulis blok kode

```
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

*html.Div* merupakan komponen html dalam Dash Plotly yang fungsinya sama dengan *div* pada HTML yaitu digunakan sebagai kontainer elemen HTML yang lain. *html.H2* kode ini digunakan untuk membuat layaknya heading H2 pada HTML. Komponen H2 ini ada dalam modul html. Untuk menampilkan grafik kita memerlukan objek *Graph* yang berada pada modul *dcc*. Pada kode di atas kita akan membuat line chart dengan menggunakan objek dari *scatter plot* . *figure* pada kelas Graph diisi dengan objek Figure dari *graph_objects*, dan argumen untuk kontruktor dari *go.Figure* diisi dengan *go.Scatter* yang sebenarnya kita akan membuat grafik dengan tipe *scatter plot*. Namun dengan menggunakan *mode=lines+markers+text* akan membuat grafik tersebut menjadi sebuah Line Chart, sekaligus memberikan *marker* bulat dan text label. Argumen *text* berisi *list* dari text label yang akan ditampilkan. Nilai *x* dan *y* axis disi dengan sebuah list yang mempunyai panjang yang sama. Misalkan x adalah *list* nama daftar bilangan dan y adalah *list* hasil pangkat 2 dari bilangan tersebut. Pada kode di atas akan muncul Line Chart yang memiliki text label berupa keterangan dari bilangan simbol pangkat 2.

## Menjalankan Kode

Kode secara utuh akan tampil sebagai berikut.

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


Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *line_chart_with_text_label.py*) lalu kita jalankan dengan perintah.

```
$ python line_chart_with_text_label
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.

![Tampilan]({{ site.baseurl }}/assets/images/line_chart_with_text_label.png)
