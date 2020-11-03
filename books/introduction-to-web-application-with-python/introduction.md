---
title: "はじめに"
---

# Change Log
2020年10月21日　執筆開始。
2020年10月25日　「はじめに」を書いた。
2020年10月25日　「Webアプリケーションとは何か？」を書いた。
2020年10月25日　「へなちょこWebサーバーを作る」を書いた。
2020年10月26日 　「STEP1: ChromeとApacheで通信してみる」を書いた。
2020年10月27日 　「STEP2: Chromeと自作サーバーで通信してみる」を書いた。
2020年10月29日 　「STEP3: 自作クライアントとApacheで通信してみる」を書いた。
2020年10月29日 　「STEP4: 自作サーバーを進化させる」を書いた。

# 本書の目的と進め方
本書の目的は、Pythonを使ってWebアプリケーションを自作することにより、**フレームワーク**や**Webサーバ**と呼ばれる、Webエンジニアであれば普段からよく使うプログラムの挙動について理解を深めることです。

本書では、自作するプログラムをできるだけ小さなステップで進化させ、常に「稚拙だけど、それだけで動くもの」として徐々にWebアプリケーションっぽく近づけていく進め方を意識しています。

初めから世の中に出回っているような立派なWebアプリケーションを作ろうとするのは、勉強の観点からはあまり得策ではありません。
データベースやルーティング、テンプレートエンジンなど、Webアプリケーションを構成する要素は多く、それぞれの技術トピックは深く議論され綿密に作り込まれており、まともなものを作ろうと思うと1機能を作るだけで心が折れてしまうこと間違いなしだからです。

ですので、その時々で最も大事で必要な機能だけを、「小さくかっこ悪く」つけ足していき、だんだんWebアプリケーション**っぽく**なっていくような進め方をとります。
ソースコードも、最初は稚拙なアプローチでいわゆる「ベタ書き」のような書き方をしながら作っていきます。
[YAGNIの法則](https://ja.wikipedia.org/wiki/YAGNI)に従い、必要になったとき（同じソースコードが何回も出現する、ソースコードが長すぎて見通しが悪くなった）に初めてリファクタリングしながら進めます。
そうすることで、「かっこよくはないけど、自分でイチから書いた、なぜ動くかがよく分かる」プログラムになると思うからです。

# 本書の対象読者
一般的なWebフレームワーク（`Laravel`, `Django`, `Ruby on Rails`, `Spring`など）を使って、Webサービスを開発した経験があり、かつフレームワークやWebサーバーといった基盤技術についての知識にあまり自信のない方を想定読者としています。
ですが、Webフレームワークを使ったことがない方も、「何が起きているか」は分かるような構成になっていると思いますので、是非チャレンジしてみてください。
（「何が便利なのか」は、実際にWebフレームワークを使ってサービスを作ってみないと分からないかもしれません）

また、本書ではPython3を使って開発を進めるため、Python3における一般的な文法は既知として進めます。
具体的には、`for文`や`while文`、`try-catch文による例外処理`、`with文によるファイルの読み書き`などのレベルが分かることを前提とします。

自信のない方は[python tutorial](https://docs.python.org/ja/3/tutorial/)に目を通してみてください。

python特有の込み入った（pythonicな）機能は極力使わないよう心がけますが、どうしても使う場合にはその都度補足をいれます。

# 本書の動作環境
筆者は下記環境で動作確認を行っています。

|        | バージョン                       |
| ------ | ----------------------------- |
| OS     | MacOS Catalina 10.15.7        |
| Python | 3.8.2                         |
| CPU    | 2.8 GHz クアッドコアIntel Core i7 |
| メモリ   | 6 GB 2133 MHz LPDDR3          |

## OSについて
本書では、MacOSを利用している前提で進めていきます。

しかし、WindowsやLinuxでは動作しないPythonライブラリやアプリケーションは使用しません。
Apacheのインストール等ではOSによって手順が変わるとは思いますが、現在はインターネット上に様々な情報がありますので代替手順はすぐに見つかると思います。

そういった各OSごとの手順を網羅して紹介することも可能ですが、こういうものはすぐに古くなってしまいますので、本書では極力紹介しない方針で進めていきます。
（MacOSの手順ですら省略するかもしれません。）

手順が分からなければ、お気軽に[サポートサイト](https://github.com/bigen1925/python_web_application_for_3rd_year_engineer)からお問い合わせください。

## Pythonについて
Pythonのバージョンには気をつけてください。
厳密な必須環境の確認はしていませんが、すくなくとも**Python 3.5以上**でないと動かないはずです。

Pythonのバージョンは、コンソールで`python -V`とすると確認できます。
```
$ python -V
Python 3.8.2+
```

自分のPCのPythonのバージョンが古い、または本書の実習のみ別バージョンを使いたい、などといった方は `Python バージョン管理`などでググってみてください。
具体的な手順や参考サイト等はあっという間に古くなってしまうので、ここでは割愛させていただきます。

特定のOSでうごかないライブラリ等は使用しませんが、ファイルパスの処理などは適宜読み替えて動かしていただく必要があるかもしれません。

手順が分からなければ、お気軽に[サポートサイト](https://github.com/bigen1925/python_web_application_for_3rd_year_engineer)からお問い合わせください。

## メモリ/CPUについて
念の為掲載しましたが、本書を進めるにあたってメモリやCPUリソースが問題になることはない想定です。


# 本書で扱うソースコードについて
本書で扱うソースコードはすべて
https://github.com/bigen1925/python_web_application_for_3rd_year_engineer
こちらに掲載しています。

ソースコードの転載、引用、改変は無償かつ無制限、無許諾にて行って構いませんが、それらを不特定多数へ公開する場合は出典の明記をお願いします。

# 本書内容の不明点について
[上記リポジトリ](https://github.com/bigen1925/python_web_application_for_3rd_year_engineer)にて、`question`ラベルのissueを作成していただくか、下記の筆者連絡先までご連絡ください。


# 筆者について
連絡先: https://twitter.com/bigen_1925

ぺーぺーのエンジニアです。

新卒未経験でITベンチャーに就職し、自社開発Webサービスに携わりながら、現在5年目3社目です。

直近は某電力系ベンチャーにて新規事業の技術リードを行い、インフラ〜バックエンド、認証等の設計/実装を行うなどしていました。

オンラインブックとはいえ、初めての書籍執筆になるので、少し緊張していますが、楽しみです。


