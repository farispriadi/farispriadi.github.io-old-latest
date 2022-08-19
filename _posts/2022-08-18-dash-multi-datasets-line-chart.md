---
layout: post
title:  "Line Chart dengan Multi Datasets"
author: faris
categories: [ dash, plotly, line chart, tutorial ]
image: https://images.pexels.com/photos/590011/pexels-photo-590011.jpeg
---
Pada post kali ini kita akan mencoba membuat line chart dari dua datasets yaitu bilangan pangkat 2 dan bilangan pangkat 3.

## Impor Modul

```
import dash
from dash import html
from dash import dcc
from plotly import graph_objects as go


```
Beberapa modul yang kita perlukan antara lain *html* untuk mengakses kelas-kelas komponen HTML, *dcc* untuk mengakses kelas-kelas komponen interaktif, dan *graph_objects* untuk mengakses kelas untuk membuat grafik

## Membuat Figure Line Chart Dengan 2 Garis

```
import dash
from dash import html
from dash import dcc
from plotly import graph_objects as go

fig = go.Figure()

fig.add_trace(go.Scatter(
					x = [1,2,3,4],
					y = [1,4,9,16],
					mode='lines',
					name='Pangkat 2'
				)
			)


fig.add_trace(go.Scatter(
					x = [1,2,3,4],
					y = [1,8,27,64],
					mode='lines',
					name='Pangkat 3'
				)
			)

fig.update_layout(title='Bilangan Berpangkat')




```

Objek *Figure* kita buat dan dimasukkan ke dalam variabel *fig*. Dengan menggunakan method *add_trace* kita bisa menambahkan dataset ke dalam objek *Figure*. Untuk menambahkan judul dari grafik, gunakan method *update_layout* dan argumen dengan kata kunci *title*. 

## Membuat Objek Dash


```
import dash
import dash
from dash import html
from dash import dcc
from plotly import graph_objects as go


fig = go.Figure()

fig.add_trace(go.Scatter(
					x = [1,2,3,4],
					y = [1,4,9,16],
					mode='lines',
					name='Pangkat 2'
				)
			)


fig.add_trace(go.Scatter(
					x = [1,2,3,4],
					y = [1,8,27,64],
					mode='lines',
					name='Pangkat 3'
				)
			)

fig.update_layout(title='Bilangan Berpangkat')


app = dash.Dash(__name__)

app.layout = html.Div([
				# Div utama
				html.Div([
					# Div untuk Judul
					html.H2("Line Chart Dengan Multi Datasets")
				]),
				html.Div([
					# Div untuk Line Chart
					dcc.Graph(figure= fig
					)
				]),
			])

if __name__ == '__main__':
	app.run_server()

```

Selanjutnya kita perlu membuat objek *Dash* yang disimpan dalam variabel *app*. Untuk membuat layout pada objek *Dash*, gunakan atribut *layout*. Dari kode di atas terdapat *div* yang bisa dikatakan sebagai kontainer utama. Dari kontainer utama tersebut dibagi menjadi 2 *div* lagi. *Div* pertama untuk judul dari aplikasi *Dash* dan yang kedua untuk meletakkan objek grafik.

## Menjalankan Kode


Kita dapat menjalankan kode dengan menyimpannya terlebih dahulu (misalkan dengan nama file *line_chart_multi_datasets.py*) lalu kita jalankan dengan perintah.

```
$ python line_chart_multi_datasets.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```


Anda bisa buka browser dan arahkan ke url *http://127.0.0.1:8050*.

![Tampilan]({{ site.baseurl }}/assets/images/line_chart_multi_datasets.png)
