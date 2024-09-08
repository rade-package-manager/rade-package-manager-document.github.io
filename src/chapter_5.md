# rade list 

rade listはインストールできるパッケージを一覧出力します
<br>
また、listは\-iオプションをつけることで、インストールしているパッケージを表示します
<br>
例：rade list
```bash
❯ rade list
hello_knife
pravda
kajisp
noze
endolphine
build_error
stack-lang
scriptS
```
これらは現在インストールできるパッケージの一覧です(2024年9月現在)
<br>

`rade list -i`:
```bash
❯ rade list -i
pravda
rade
hello
```
これらは私がインストールしているパッケージです。
<br>

## 何が行われているのか
rade list時に行われていることは、packagelistディレクトリを読み込み、
ディレクトリが存在したら、そのディレクトリ名を出力するという仕組みです。
<br>
\-iオプションのとき実行されていることは、\~/.comrade/bin/の中身を読み取り、その内容を出力しているだけです
<br>
<br>
<br>

これでこのチャプターは終わりです。





