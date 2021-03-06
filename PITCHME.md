@transition[none]
# @css[headline](GEOSPATIAL Hackers Program Hands-on)

---
@snap[top]
@css[agenda](アジェンダ)
![logo](assets/img/logo.png)
@snapend

@snap[west]
@css[agenda](1.WebGISを作ろう)<br/>
@css[agenda](2.GISとは)<br/>
@css[agenda](3.地理空間情報とは)<br/>
@css[agenda](4.WebGISとは)<br/>

@snapend

---

## オープンデータを利用して、WebGISを使った地図アプリを作ろう。

---

## WebGISを作ろう

---
## GISとは


> 地理情報システム（GIS：Geographic Information System）は、地理的位置を手がかりに、位置に関する情報を持ったデータ（空間データ）を総合的に管理・加工し、視覚的に表示し、高度な分析や迅速な判断を可能にする技術である。

[国土交通省国土地理院HP](http://www.gsi.go.jp/GIS/whatisgis.html)より引用

---
## 地理空間情報とは

> 地理空間情報とは、空間上の特定の地点又は区域の位置を示す情報（位置情報）とそれに関連付けられた様々な事象に関する情報、もしくは位置情報のみからなる情報をいう。

[国土交通省国土地理院HP](http://www.gsi.go.jp/GIS/whatisgis.html)より引用

---
##  WebGISとは

WebGISは、インターネット技術を使用したGISのことです。




---
## 準備

---
## インストールが必要なもの
1. テキストエディタ
1. Elixir
1. node.js
1. PostgreSQL
1. Phoenixframework

---
## エディタのインストール

テキストエディタ、普段ご利用のものをお使いください。

入ってない方は、この講座では以下を利用しています。

[VSCODE](https://code.visualstudio.com/)<br/>

---
## アドインの追加
VSCODEにElixirのアドインを追加します。

[MarketplaceよりElixirのアドイン追加](https://marketplace.visualstudio.com/items?itemName=mjmcloug.vscode-elixir) 

![Elixirのアドイン追加](assets/img/vscode-elixir.png)

---
## ターミナルからエディタを起動するための準備
VSCODEを開いた状態で

Command + Shift + P で検索窓を開きます。

![vscodeのアドイン追加](assets/img/vscode-adin.png)

---

「Shell」を検索し、インストールします。

![vscodeでshellを検索](assets/img/vscode-shell.png)

---
## ターミナルとは

プログラミングをする際に、コマンドを用いて操作や設定などを行うためのツール

WindowsとMacで呼び名と使用するコマンドが若干異なる

* Windows->コマンドプロンプト
* Mac->ターミナル

---
## ターミナルの使い方（Mac）
現在のディレクトリ内にあるファイルやディレクトリの確認
```
ls
```

任意のディレクトリに移動する方法
```
cd  ディレクトリ名
```

新規ディレクトリ作成
```
mkdir 任意のディレクトリ名
```

---
## コマンドプロンプトの使い方（Windows）
現在のディレクトリ内にあるファイルやディレクトリの確認
```
dir
```

任意のディレクトリに移動する方法
```
cd ディレクトリ名
```

新規ディレクトリ作成
```
md 任意のディレクトリ名
```
mkdirでも作成可能

---
## ターミナルからエディタを起動する方法
cd コマンドを使用しプロジェクトで使用するディレクトリに移動します
```
cd ディレクトリ名
```

移動後に、下記のコマンドで起動します
```
code .
```

VSCODEが起動すればOK

---
## エディタをターミナルから開く方法

エディタを開き
Command + Shift + Pでコマンドパレット開く。
「Shell」を検索しインストール。

ターミナルから```codeで```起動できます。

---
## Elixirのインストール
今回は、Elixirという言語を利用しますので

お使いの環境に合わせて、インストールしてください。

[Elixirのインストール方法](https://elixir-lang.org/install.html)

elixirに必要なパッケージ類も一緒にインストールされます。

---
## Macの場合
homebrewを使用すると便利です。

[homebrewのインストール方法](https://brew.sh/index_ja)

![MacでElixirのインストール](assets/img/elixir-install-mac.png)

---
インストール後homebrewをアップデート
```
brew update
```
アップデート後、下記コマンドでElixirのインストール
```
brew install elixir
```
---
## Windowsの場合
![WindowsでElixirのインストール](assets/img/elixir-install-win.png)

[Elixirのインストール方法](https://elixir-lang.org/install.html)内 Windowsの「Download the installer」

よりインストール。

---
## Elixirとは

> Elixir (エリクサー) は並行処理の機能や関数型といった特徴を持つ、Erlangの仮想マシン (BEAM) 上で動作するコンピュータプログラミング言語である。

引用元 [Wiki](https://ja.wikipedia.org/wiki/Elixir_(%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E8%A8%80%E8%AA%9E))

---
## node.jsのインストール

https://nodejs.org/en/download/


---
## PostgreSQLのインストール

DBにPostgreSQLを利用します。まだインストールされてない方は以下より

[インストーラーでインストール](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads)<br/>

ご利用の環境に合わせてダウンロードください。<br/>
今回は、version 11.1 をダウンロードします。

* パスワードはpostgresを設定します。

---
## Phoenixframeworkのインストール

Webのフレームワークとして、Phoenixを利用

[Phoenix](https://hexdocs.pm/phoenix/installation.html)<br/>

---
* Windows->プロンプト
* Mac->ターミナル

より、以下を入力してください。

```
mix archive.install hex phx_new 1.4.0
```
Phoenixがインストールされます。

---
## Serverを立ち上げよう
まずプロジェクトを作成します
```
mix phx.new sample
```
sampleの部分がプロジェクト名になります。

```
Fetch and install dependencies? [Yn] 
```
上記がターミナルに表示されたら　yを入力しEnter。

---
## Serverを起動しよう！
作成したプロジェクトフォルダに移動します。
```
cd sample
```
プロジェクトフォルダに移動できたら
```
iex -S mix phx.server
```
上記コマンドを入力、serverを起動します。

---
serverを起動したら、
ブラウザで「`http://localhost:4000`」にアクセス。

Phoenixで作られたデフォルトのWebページが表示される事を確認しましょう。

無事に見られたら、成功です。

---
## Mapの作成

---

#### [reaflet.js](https://leafletjs.com/)

lib/App名_web/template/layout/app.html.eex

---
```html
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

@[7-8](app.html.eexの<head>タグの中にCDNを追加する)
@[9-18](styleを追加する)

---

lib/App名_web/template/page/index.html.eex

---

```html

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

---
mix.exs

```elixir
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
@[15](smallexのモジュールを追加)

---
## 外部APIの取得

---

lib/App名_web/template/layout/app.html.eex
```html
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
@[6-8](Vue.jsとAxiosのCDNを追記)
---

## APIの作成
---

コンソール上で

```elixir

mix phx.gen.json Api Location locations lng:float lat:float pointname:string

```

---

```elixir
Add the resource to your :api scope in lib/test_web/router.ex:

    resources "/locations", LocationController, except: [:new, :edit]

Remember to update your repository by running migrations:

    $ mix ecto.migrate

```
@[3](lib/test_web/router.exに追記する)

---

lib/test_web/router.ex

```elixir
#...省略
  scope "/", TestWeb do
    pipe_through :browser

    get "/", PageController, :index
    resources "/locations", LocationController, except: [:new, :edit] #<- 追加
  end
#...省略
```
@[6]
---

```elixir
Add the resource to your :api scope in lib/test_web/router.ex:

    resources "/locations", LocationController, except: [:new, :edit]

Remember to update your repository by running migrations:

    $ mix ecto.migrate

```
@[7](コンソールに戻り、migrateする)

---
```elixir
iex -S mix phx.server
```
@[1](コンソールからサーバーを起動します。)

---

REST APIクライアントを使って、データをインプットやアウトプットする
今回は、Firefoxの「RESTClient」を利用して説明します。
* [「Firefoxのダウンロード」](https://www.mozilla.org/ja/firefox/new/)はこちら
* [Firefox「RESTClient」](https://addons.mozilla.org/ja/firefox/addon/restclient/)
* [Chrome「Postman」](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)

---

## 内部APIを呼び出し

---

## 表示
```html

<h1>Location</h1>
<table border="0">
<tr v-for="(result, index) in results">
    <td style="padding: 10px;">{{ result.lng }}</td>
    <td style="padding: 10px;">{{ result.lat }}</td>
    <td style="padding: 10px;">{{ result.pointname }}</td>
</tr>
</table>

<script>

    var app = new Vue
    ( {
        el: '#app',
        data: 
        {
            results: [],
        }, 
        mounted()
        {
            axios.get( '/locations' )
            .then( response => { this.results = response.data.data } )
        },
    } )
</script>
```

---
## 追加・更新・削除の作成

```html
<h1>Location</h1>
<table border="0">
<tr v-for="(result, index) in results">
    <td style="padding: 10px;"><input type="text" v-model="result.lat"></td>
    <td style="padding: 10px;"><input type="text" v-model="result.lng"></td>
    <td style="padding: 10px;"><input type="text" v-model="result.pointname"></td>
</tr>
</table>
<button v-on:click="onUpdate">全件更新</button>

<script>

    var app = new Vue
    ( {
        el: '#app',
        data: 
        {
            results: [],
        }, 
        mounted()
        {
            axios.get( '/locations' )
            .then( response => { this.results = response.data.data } )
        },
        methods:
        {
          onUpdate: async function( evt )
          {
            this.results.forEach( ( result, i ) => 
            {
              axios.put( '/locations/' + result.id,
              {
                  'location':
                  {
                    'lat': result.lat,
                    'lng': result.lng,
                    'pointname': result.pointname
                  }
              })
            })
          },
    } )
</script>
```

@[5-7]
@[10]
@[14-30]
---
## DB操作を作成

---

lib/util/db.ex
```elixir

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
@[4](Test.Repoは自分のApp環境の名前に合わせる)

---

```SQL

# \dt

# SELECT * FROM locations; 
  
```
@[4]
---
## Mapへのポイント追加との連携

---
## 2点間の距離を求める

---

lib/App名_web/template/layout/app.html.eex
```html

<!DOCTYPE html>
<html lang="en">
  <head>

    //...省略

    <script src="http://cdn.leafletjs.com/leaflet-0.7.3/leaflet.js"></script>
    //以下を追加
    <script src='//api.tiles.mapbox.com/mapbox.js/plugins/turf/v1.4.0/turf.min.js'></script> 

    //...省略

  </head>

```
@[10]

---
利用サービス
* [leafletjs](https://leafletjs.com)
* [国土地理院](https://maps.gsi.go.jp)
* [TURF](http://turfjs.org/getting-started/)
* [Firefox「RESTClient」](https://addons.mozilla.org/ja/firefox/addon/restclient/)

---
利用技術の紹介
* [Elixir](https://elixir-lang.org/)
* [Phoenix](https://phoenixframework.org/)
* [PostgreSQL](https://www.postgresql.org/)
* [Vue.js](https://jp.vuejs.org/index.html)

---
オープンデータ

---
参考情報
* [OpenStreetMap](https://openstreetmap.jp)
* [CART](https://carto.com/)
* [SPARQL](https://www.slideshare.net/uedayou/web-apisparql)
* [QGIS](https://www.qgis.org/)
* [地図tile](https://wiki.openstreetmap.org/wiki/JA:%E3%82%BF%E3%82%A4%E3%83%AB)