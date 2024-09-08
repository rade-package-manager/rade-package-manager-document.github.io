# rade upgrade

comradeはradeと省略します
<br>

`rade upgrade`は、rade自身を最新に保ちます。
<br>
これを実行すると、radeは自分自身を再構築し、新しいradeとして生まれ変わります。
<br>
では、upgrade時に何が行われているのか見てみましょう
<br>
<br>

では、あなたが`rade upgrade`と入力したと仮定しましょう。
<br>
そうすると、radeは、自分の最新バージョンが何かを確認しに行きます。
<br>
もし、radeの最新バージョンが現在のバージョンと同じだった場合、radeはそのまま何もせず、ユーザーへ、"radeはすでに最新です"と表示します
<br>
では、radeの最新バージョンが現在のバージョンより上だった場合はどうでしょう。
<br>
その場合、radeは自分をアップグレードします。
<br>
アップグレードの工程を見てみましょう。
<br>
まず、radeはbuildディレクトリが存在していた場合、buildディレクトリを削除します。
<br>
buildディレクトリが削除された、もしくは存在していなかった場合、radeはbuildディレクトリへ[自分](https://github.com/rade-package-manager/rade-package-manager)をクローンします
<br>
次に、radeはpackagelistを更新します。アップグレード時、radeを完全に最新に保つためです
<br>
パッケージリストの更新が終わると、radeはmakeを使用して自分自身をビルドします。
<br>
こうすることで、どの環境でもradeが動くためです
<br>
makeが終了し、すべてが正常に終了すると、アップグレードは無事に終了します。
<br>
こうすることで、radeはアップグレードを実現しているわけです。
<br>
<br>

これでこのチャプターは終了です。次は、
<br>
`rade install`の説明です。
<br>




