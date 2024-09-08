# rade install <package>

install機能は、パッケージマネージャーになくてはならない機能です。
<br>
radeは、インストール時、依存関係,容量,使用している言語などを取得します。
<br>
では、あなたが`rade install hello_knife`と入力したとき、radeが何をしているのか見てみましょう
<br>
<br>

## パッケージが存在するかの確認

インストール対象のパッケージが存在するか確認します(今回の場合はhello_knifeが存在するかの確認)
<br>
packagelist内のディレクトリをすべて確認し、hello_knifeというディレクトリが存在する場合はインストールを続行し、存在しない場合は、"そのようなパッケージはありません"という旨の文字列を出力します。
<br>

## 存在していた場合

存在していた場合、radeはパッケージのディレクトリ内にある
<br>
dependenciesファイル,languageファイル,repositoryファイル,capacityファイル,versionファイルを読み取ります
<br> 

その後、radeはrepositoryファイル内にあるレポジトリurlを読み取り、そのレポジトリをクローンします。
<br>

## クローンに成功した場合

radeがクローンに成功すると、radeはそのレポジトリ内に.comradeというディレクトリが無いか探します。
<br>
もし.comradeというディレクトリが存在した場合、radeは.comradeディレクトリの中にある、exec_nameというファイルを読み取ります。
<br>
そのファイルの中には、そのレポジトリをコンパイルしたあとの実行可能ファイルの名前が入っています
<br>
そのファイルを読み終えると、radeはそのレポジトリにあるinstall.shを実行します。
<br>
もし.comradeが存在しなかった場合は、実行可能ファイル名はレポジトリ名だとradeは予測し、install.shを実行します。
<br>
install.shは、そのレポジトリのコンパイル方法が記入されているシェルスクリプトであり、radeのプログラムインストールに欠かせないものです。
<br>

## プログラムのコンパイル
radeは、コンパイルのためにinstall.shを実行します。
<br>
install.shが異常終了した場合、radeは実行を停止し、エラーメッセージを出力します。
<br>
この異常終了を体験できるパッケージが一つ存在します。
<br>
それは、`build_error`パッケージです。
<br>
build_errorパッケージをインストールしようとすると、意図的にコンパイルエラーが発生し、ビルドが中止、更にはradeも停止します。気になる方はインストールしてみてください。
<br>
(直したら面白いことが起きるという噂が...)
<br>
閑話休題
<br>

radeは、ビルドが無事に終了すると、実行可能ファイルが無いか探します。
<br>
実行可能ファイルがある場合、radeは\~/.comrade/bin/にプログラムを移動させ、ログを書き込み、無事にインストールが終了します。
<br>
もしプログラムが存在しなかった場合、radeはエラーを起こし、異常終了します。
<br>
(プログラムが存在しなかった場合の処理は、.expect()で処理されています)
<br>
インストールが終了すると、radeはビルドディレクトリを消去し、次のインストールに備えます。
<br>
<br>
以下は、hello_knifeパッケージをインストールしたradeのログです
```bash
❯ rade install hello_knife
>>> removing build directory... # buildディレクトリが存在していた場合は削除する
>>> Clone package... # hello_knifeという名前のパッケージが見つかったため、repositryファイルを読み取り、クローンする
install package: hello_knife
executable file name: hello # .comradeというディレクトリが存在していたため、そのディレクトリの中にあるexec_nameを読み取り、出力する
capacity: bytes # capacityファイルを読み取り、出力する。(なお、hello_knifeのcapacityファイルが空っぽのため、bytesとだけ表示されている)
language: C # hello_knifeはC言語で書かれているため、Cと表示される
versions: v1.0 # hello_knifeのバージョンを出力する
dependencies: None # hello_knifeの依存関係は何も無いためNoneと表示される
repository: https://github.com/knife-package-manager/hello_knife #  hello_knifeのレポジトリurl

install hello_knife?
[y/n] y
>>> Start Installation
>>> run install.sh (build start) # install.shを実行し、ビルドを開始する
>>> build end # install.shが正常終了
>>> moving file... # 実行可能ファイルを~/.comrade/bin/に移動させ、実行できるようにする
>>> remove build directory... # buildディレクトリを削除
>>> Fill in the log... # インストールしたものをlogに書き込む
/home/inado/.comrade/log/install/hello_knife
All done! # インストールは正常に終了され、すべて完了したことを知らせる
Installation is complete
For more information on hello_knife, please see https://github.com/knife-package-manager/hello_knife.
```

<br>
<br>
これでこのチャプターは終わりです。次はlistの説明です
