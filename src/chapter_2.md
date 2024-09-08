# rade update

`rade update`は、comradeのパッケージリストを更新します。
<br>
comradeのパッケージリストは、~/.comrade/packagelist/にあります。
<br>
updateを実行すると、comradeは一度packagelistを削除し、[comradeのパッケージリスト](https://github.com/rade-package-manager/rade-package-list)をクローンします。これによって、packagelistはすべて最新になります。
<br>
もし、\~/.comrade/packagelist/が見つからなかった場合は、packagelistをクローンし、パッケージリストを最新にするだけです
<br>

### もしpackagelistを更新できなかった場合

packagelistをクローンできなかった場合、comradeはエラーメッセージを出力し、そのまま動作を停止します。
![クローンできなかった場合のエラーメッセージ](../Failed-clone-packagelist.png)
(このエラーメッセージは、インターネット接続がされていないため発生したエラーメッセージです。)
<br>

### パッケージの内容

パッケージの内容は以下のようになっています
```sh 
❯ tree hello_knife/
hello_knife/
├── capacity
├── dependencies
├── language
├── repository
└── version

1 directory, 5 files
```
(hello_knifeパッケージを使用しました)
<br>
それぞれ見ていきましょう
<br>

- **capacity**
<br>
そのパッケージの容量を示すファイルです。
<br>
comradeはインストール時capacityファイルを見て、容量を表示します

- **dependencies**
パッケージの依存関係を示すファイルです
<br>
インストール時、このファイルを見て依存関係を確認します
<br>
(最も、現在のcomradeに依存関係の解決機能は無いですが、、、)

- **language**
<br>
そのパッケージが使用しているプログラミング言語が記入されています。
<br>
hello_knifeの場合は、C言語を使用しているため、このファイルに記入されるものは`C`です

- **repository**
<br>
そのパッケージのレポジトリurlが記入されているファイルです。
<br>
comradeは、インストール時にこのファイルを確認し、ターゲットレポジトリをクローンします。

- **version**
<br>
そのパッケージのバージョンが記入されているファイルです。
<br>
comradeは、インストール時このファイルを確認し、出力します。

### もしパッケージを新しく作りたい場合
[rade-package-list](https://github.com/rade-package-manager/rade-package-list)に、create_package.bashという実行可能シェルスクリプトが存在します。
<br>
そのシェルスクリプトを実行すると、かんたんにパッケージを追加できます。
<br>
例(追加するパッケージが"test-package"の場合)：
```bash
./create_package.bash test-package None rust hxxps://github.com/test-package/rade-test-package 100 v1.0
```
それぞれ何を意味しているのか見てみましょう
<br>

- **test-package**
<br>
パッケージ名です。
<br>
この名前のパッケージ(ディレクトリ)が生成されます

- **None**
<br>
依存関係です。
<br>
何も依存していない場合はNone、もしくは空白でもいいです。

- **rust**
<br>
このパッケージに使用しているプログラミング言語です。
<br>
今回、test-packageはRustを使用している想定なので、ここに書かれるのはrustです。
<br>
(言語名は小文字にしてください)

- **hxxps://github.com/test-package/rade-test-package**
<br>
レポジトリurlです。このレポジトリがクローンされ、インストールされます。
<br>

- **100**
<br>
パッケージのプログラムが使う容量です。
<br>
今回は100にしました。
<br>
(なお、comradeの容量表記はbytesです。つまり100と入力すると、100bytesのプログラムということです)
<br>

- **v1.0**
<br>
プログラムのバージョンです。このバージョンをインストール時に出力します。
今回はversion1.0ということにしました


<br>
<br>
<br>

これでこのチャプターは終わりです。
<br>
次のチャプターはrade upgradeの説明です
