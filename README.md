# 構成

| No | サービス | ホスト側ポート | コンテナ側ポート | 備考 |
|:--|:--|:--|:--|:--|
| 1 | Nginx | 21337 | 80 | Fluentd のテストのために導入しているだけ.<br/>No 2 の 24224 へログを送る. |
| 2 | Fluentd | 24224 | 24224 | 受信したログを No 3 へ送る |
| 3 | Fluentd | 34224 | 34224 | 受信したログを stdout へ出力する.<br/>Elasticsearch との連携はまだである.<br/>最終的には Nginx のログを Elasticsearch に送り込む.|
| 4 | Elasticsearch | 29200 | 29200 | ログ格納のためのデータストア.<br/>日本語検索をするための kuromoji 導入あり |
| 5 | Kibana | 29601 | 29601 | Elasticsearch 閲覧 |

![image](https://user-images.githubusercontent.com/86971991/128673300-6a2ba969-6c0c-4fc1-85fc-d22261379f0e.png)

　

# 起動方法

```
$ docker-compose up -d
もしくは
$ docker-compose build --no-cache
$ docker-compose up -d
```

　

# 参考にした書籍およびサイト

|書籍|
|:---|
|[nginx実践入門](https://gihyo.jp/book/2016/978-4-7741-7866-0)|
|[「Docker/Kubernetes 実践コンテナ開発入門  山田 明憲」](https://gihyo.jp/book/2018/978-4-297-10033-9)|
|[データ分析基盤構築入門［Fluentd，Elasticsearch，Kibanaによるログ収集と可視化］](https://gihyo.jp/book/2017/978-4-7741-9218-5)|
|[検索だけじゃない Elasticsearch 入門+](https://booth.pm/ja/items/1031664)|


|URL|一言|
|:--|:---|
|https://qiita.com/sanyamarseille/items/1c4c31547502791ecac6||
|https://www.elastic.co/guide/en/elastic-stack-get-started/current/get-started-docker.html||
|https://qiita.com/suzuki_y/items/6365799485fa3973b916||
|https://qiita.com/sugikeitter/items/f3b2c57bf8bbdc47a8bc||
|https://github.com/sugikeitter/elasticsearch-kibana-docker/blob/master/docker-compose.yml||
|https://gitya107.hatenablog.com/entry/2018/06/15/170334||
|http://ittoo.jugem.jp/?eid=737||
|https://qiita.com/kaibadash@github/items/9cfb532696dc8711e408|日本語検索を可能にする|
|https://qiita.com/mserizawa/items/8335d39cacb87f12b678|日本語検索を可能にする|
|https://github.com/deviantony/docker-elk|ELK を構築するための docker-compose が公開されている|
|https://dev.classmethod.jp/articles/es-01/|index, document, type の説明が簡潔に RDMS に例えられていて良かった|
|http://www.tech-joy.work/article/a20180527115811.html|/etc/elasticsearch/elasticsearch.yml の記述例と説明あり|
|https://qiita.com/Esfahan/items/3c07bfbb57c7098e9531|3台に Elasticsearch を導入した場合の手順あり|

