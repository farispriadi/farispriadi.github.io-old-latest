---
layout: post
title:  "Membuat Bar Chart dengan Dash Plotly."
categories: [ dash, plotly, bar chart, tutorial ]
image: https://images.pexels.com/photos/590020/pexels-photo-590020.jpeg
---

Bar chart atau diagram batang digunakan untuk menampilkan data yang berkategori. Dengan menggunakan Dash Plotly kita bisa dengan mudah membuat Bar Chart. Berbeda denga Line Chart, untuk membuat Bar Chart, kita akan membutuhkan *plotly graph objects*.


## Import modul yang diperlukan

Untuk membuat bar chart sederhana, kita memerlukan beberapa modul dalam dash plotly.

```
import dash
from dash import html
from dash import dcc
from plotly import graph_objects as go


```

*import dash* digunakan untuk mengimpor modul dash. *from dash import html* digunakan untuk mengimpor html dash atau *dash html components*, komponen ini memungkinkan kita memasukkan komponen HTML dengan menggunakan sintaks python. *from dash import dcc* digunakan untuk mengimpor komponen core dari dash atau *dash core components* yang digunakan untuk memasukkan komponen interaktif termasuk membuat grafik. Untuk bar chart kita memerlukan *plotly graph object* karena dalam *dcc.Graph* hanya menyediakan Line Chart dan Scatter Plot.

## Membuat Layout

Selanjutnya kita akan membuat layout atau tata letak.

```
import dash
...


from plotly import graph_objects as go

app = dash.Dash(__name__)

app.layout = html.Div([
				# Div utama
				html.Div([
					# Div untuk Judul
				]),
				html.Div([
					# Div untuk Bar Chart
				]),
			])

```

*app = dash.Dash(\_\_name\_\_)* kode ini adalah langkah awal kita untuk membuat objek dash yang disimpan dalam variable *app*. Selanjutnya *app.layout*, kita akan meng-assign atau memasukkan layout kita ke dalam atribut layout yang berada di dalam *app*. Layout tersebut akan kita buat dengan satu *Div* utama dan di dalamnya terdapat dua *Div* anakan. Dimana *Div* pertama untuk meletakkan judul dan *Div* kedua untuk meletakkan grafik. Tanda *#* merupakan *comment* yang digunakan sebagai keterangan saja.

## Menuliskan konten

Selanjutnya kita akan menambahkan judul dan grafiknya

```
import dash
...

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
```

*html.H2* kode ini digunakan untuk membuat layaknya heading H2 pada HTML. Komponen H2 ini ada dalam modul html. Untuk menampilkan grafik kita memerlukan objek *Graph* yang berada pada modul *dcc*. Pada kode di atas kita akan membuat bar chart sederhana . *figure* pada kelas Graph diisi dengan objek Figure dari *graph_objects*, dan argumen untuk kontruktor dari *go.Figure* diisi dengan *go.Bar* untuk secara spesifik membuat bar chart. Nilai *x* dan *y* axis disi dengan sebuah list yang mempunyai panjang yang sama. Misalkan x adalah *list* nama provinsi dan y adalah *list* jumlah kabupaten dan kota dalam provnsi tersebut.

## Menjalankan Kode

Dengan demikian kode secara keseluruhan adalah sebagai berikut:

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

*app.run_server()* kode ini ditambahkan ke dalam main agar server Dash dapat berjalan. File ini akan disimpan dengan nama *simple_bar_chart.py*, Anda dapat mengganti nama sesuai dengan yang diinginkan.

Seperti kode python lainnya, untuk menjalankannya kode ini, bisa menggunakan IDE seperti PyCharm atau run di CMD  jika di windows atau Terminal jika di distibusi Linux Ubuntu. Jika menggunakan terminal maka cara menjalankan kode dari Linux Ubuntu.

```
$ python simple_bar_chart.py
Dash is running on http://127.0.0.1:8050/

 * Serving Flask app 'test' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:8050 (Press CTRL+C to quit)
```

Sekarang anda dapat membuka browser dan mengakses aplikasi dash dengan alamat url *http://127.0.0.1:8050* 
![Tampilan]({{ site.baseurl }}/assets/images/simple_bar_chart.png)