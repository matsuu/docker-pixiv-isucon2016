# docker-pixiv-isucon2016

## Overview

Pixivさんの[社内ISUCON2016](https://github.com/catatsuy/private-isu)とほぼ同じ環境を構築するためのDockerfileです。

## Usage

* Docker実行環境を用意する
* Docker Composeがあるとなお良い

### Docker Composeがあるとき

サーバ構築（省略可）

```
git clone https://github.com/matsuu/docker-pixiv-isucon2016
cd docker-pixiv-isucon2016
docker-compose build
```

build中パッケージダウンロードに失敗する場合は何度かbuildを繰り返すと良い。

サーバ構築を省略する場合は`docker-compose.yml`をダウンロードする。

サーバ起動

```
docker-compose up -d image
```

ベンチマーク実行

```
docker-compose up bench
```

しばらく待つと結果が表示される

サーバログイン

```
docker-compose exec image bash
```

サーバ停止

```
docker-compose down
```

### Docker Composeがないとき

サーバ構築（省略可）

```
git clone https://github.com/matsuu/docker-pixiv-isucon2016
cd docker-pixiv-isucon2016
docker build -t matsuu/pixiv-isucon2016-image image
docker build -t matsuu/pixiv-isucon2016-bench bench
```

build中パッケージダウンロードに失敗する場合は何度かbuildを繰り返すと良い。

サーバ起動

```
docker run -d -p 80:80 --privileged --name image matsuu/pixiv-isucon2016-image
```

ベンチマーク実行

```
docker run -it --rm --network=container:image matsuu/pixiv-isucon2016-bench -t http://127.0.0.1/
```

しばらく待つと結果が表示される

サーバログイン

```
docker exec -it image bash
```

サーバ停止

```
docker stop image
docker rm image
```

## 動作確認

Docker for Macで動作確認済です。
Docker for Windowsでも動作するかもしれませんが未確認です。

## 本来の設定と異なるところ

* 本来の競技者用サーバーはc4.large(vCPU 2, メモリ3.75GB)ですが、特に制限は行っておりません
* 本来のベンチマーカーはc4.xlarge(vCPU 4, メモリ7.5GB)ですが、特に制限は行っておりません

## FAQ

### ベンチマークがエラーになる

Docker実行環境のスペックが足りないのかもしれません。

### プログラムの動かし方がわからない

以下をご確認ください。

* [ISUCON6出題チームが社内ISUCONを開催！AMIも公開！！ - pixiv inside](http://inside.pixiv.net/entry/2016/05/18/115206)
* [catatsuy/private-isu](https://github.com/catatsuy/private-isu)
* [社内ISUCON 当日マニュアル](https://github.com/catatsuy/private-isu/blob/master/manual.md)

## TODO

* Docker Swarm対応
* もっとモダンに
* リファクタリング

## References

* [matsuu/vagrant-pixiv-isucon2016](https://github.com/matsuu/vagrant-pixiv-isucon2016)
* [matsuu/terraform-pixiv-isucon2016](https://github.com/matsuu/terraform-pixiv-isucon2016)
* [matsuu/docker-isucon](https://github.com/matsuu/docker-isucon)
