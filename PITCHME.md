# @css[headline](GEOSPATIAL Hackers Program Hands-on)

---
@transition[zoom-in fade-out]
## アジェンダ

---
1. 準備 
   1. ハンズオンのゴール
2. WebServerを構築しよう。
   1. WebServerの構成
   2. 機能要件
3. 外部APIを呼び出してみよう。
   1. モジュールの追加
4. 内部APIを呼び出してみよう。
   1. Vue + axios
5. DBにDataを入れてみよう。
---
## 準備

---
## Elixirのインストール

---
## Elixirとは

---
## PostgreSQLのインストール

---
## Phoenixframeworkのインストール

---
## Serverを立ち上げよう

---
## Mapの作成

---

#### [reaflet.js](https://leafletjs.com/)

lib/App名_web/template/layout/app.html.eex

```
<!DOCTYPE html>
<html lang="en">
  <head>

    //...省略

    <link rel="stylesheet" href="<%= Routes.static_path(@conn, "/css/app.css") %>"/>

    //以下のCSS(<style>から</style>まで）と、leaflet.jsのCDN（以下２行）を追加
    <script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>
    <link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.css">
    
    <style>
        body{
            margin: 0;
            padding: 0;
        }
        div#map{
            width: 100%;
            height: 500px;
        }
    </style>

  </head>
```

@[55-56]
@[58-67]

---

lib/App名_web/template/page/index.html.eex

```
<script>

    <div id="map"></div>
    <script>
        var map = L.map('map').setView([35.70811, 139.76268],11);
        var tileLayer = L.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{
                attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
                maxZoom: 19
            });
        tileLayer.addTo(map);

          L.marker([35.70811,139.76268]).addTo(map)
            .bindPopup('文京区')
            .openPopup();

</script>

```

---
## モジュールの導入
#### [smallex](https://hex.pm/packages/smallex)

```mix.exs

#...省略

 defp deps do
    [
     {:phoenix, "~> 1.4.0"},
      {:phoenix_pubsub, "~> 1.1"},
      {:phoenix_ecto, "~> 4.0"},
      {:ecto_sql, "~> 3.0"},
      {:postgrex, ">= 0.0.0"},
      {:phoenix_html, "~> 2.11"},
      {:phoenix_live_reload, "~> 1.2", only: :dev},
      {:gettext, "~> 0.11"},
      {:jason, "~> 1.0"},
      {:plug_cowboy, "~> 2.0"},
      {:smallex, "~> 0.1.2"},    # <- 追加
    ]
  end

#...省略


```


---
## 外部APIの取得

---

```lib/App名_web/template/layout/app.html.eex

<!DOCTYPE html>
<html lang="en">
  <head>

    //...省略
    <link rel="stylesheet" href="<%= Routes.static_path(@conn, "/css/app.css") %>"/>

    // 以下２行（Vue.jsのCDN、AxiosのCDN) を新たに追加
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.17/vue.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.18.0/axios.min.js"></script>     

    <script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>

    //...省略

  </head>

```

---

## APIの作成

---
## DBの作成

---


```lib/util/db.ex

defmodule Db do
  def query( sql ) when sql != "" do
    { :ok, result } = Ecto.Adapters.SQL.query( Test.Repo  , sql, [] )
    result
  end
  def columns_rows( result ) do
    result
    |> rows
    |> Enum.map( fn row -> Enum.into( List.zip( [ columns( result ), row ] ), %{} ) end )
  end
  def rows( %{ rows: rows } = _result ), do: rows
  def columns( %{ columns: columns } = _result ), do: columns
end

```
Test.Repoは自分のApp環境の名前に合わせる

---
## 内部APIを呼び出し

---
## 追加・更新・削除の作成

---
## Mapへのポイント追加との連携

---
## 2点間の距離を求める

---
利用サービス
[https://leafletjs.com](https://leafletjs.com)
[国土地理院](https://maps.gsi.go.jp)
[TURF](http://turfjs.org/getting-started/)

---
利用技術の紹介
[Elixir](https://elixir-lang.org/)
[Phoenix](https://phoenixframework.org/)
[PostgreSQL](https://www.postgresql.org/)
[Vue.js](https://jp.vuejs.org/index.html)

---
オープンデータ

---
参考情報
[OpenStreetMap](https://openstreetmap.jp)
[CART](https://carto.com/)
[SPARQL](https://www.slideshare.net/uedayou/web-apisparql)
[QGIS](https://www.qgis.org/)