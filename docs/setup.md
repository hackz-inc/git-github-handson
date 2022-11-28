## 事前準備

## 【GitHub のアカウント登録】

まずは、[GitHub](https://github.com)にアクセスします。  
ユーザーネーム、メールアドレス、パスワードなどの必要事項を入力し、アカウントを作成します。

## 【Git のインストール】

### Mac の場合

以下のコマンドを実行

```bash
$ brew install git
```

### Windows(git bash)

[公式サイト](https://gitforwindows.org/)からインストーラーをダウンロードします。  
ダウンロードしたインンストーラーを実行します。  
特にこだわりがない場合には、すべて「Next」を押す問題なくインストールできます。

※何をしているのか詳しく知りたい場合には、[こちら](https://www.curict.com/item/60/60bfe0e.html)を参考にしてください。

### Windows(WSL2)

以下のコマンドを実行

```bash
$ sudo apt-get install git
```

### Linux(Ubuntu)

以下のコマンドを実行

```bash
$ sudo apt-get install git
```

### インストールの確認

以下のコマンドを実行し、バージョンが表示されれば完了です！

```bash
git --version
```

ex.)
TODO: 画像の追加

## 【Git 構成ファイルのセットアップ】

先ほど作成した GitHub のアカウントと Git を紐付けます！  
以下のコマンドを実行してください。
([]で書かれている部分を自身の情報に修正してから実行してください。)

```bash
$ git config --global user.name [設定したユーザーネーム]
$ git config --global user.email [設定したメールアドレス]
```

## 【終わりに】

ここまで済んだら準備は万端です！  
お疲れ様でした！

以下のファイルに講義でよく使う用語の意味をまとめたので、こちらも合わせて見ておくとよりスムーズに進むと思います！
words.md TODO: ファイルの作成後、リンクを貼る

## 【おまけ】

ここからはやってもやらなくてもいいものなので、本人にお任せします！

### Git のエディタを変更する

コミットログを書くときに Ubuntu のデフォルトだと nano に設定されてしまうので、これを Vim に修正します。  
(Vim なのは個人的に好きなだけなので、別のものでも構いません)

以下のコマンドを実行します。

```bash
$ git config --global core.editor 'vim -c "set fenc=utf-8"'
```

### SSH 接続の設定

これを行うと、push や pull の時に**パスワード入力する手間が省けます**。  
必ずやることではないですが、やっておくと便利です。

まずは秘密鍵、公開鍵を作成します。  
鍵を入れるフォルダに移動します。

```bash
$ cd ~/.ssh
```

次のコマンドで鍵を生成します。

```bash
$ ssh-keygen -t rsa
```

何か聞かれたらエンターを三回押せば id_rsa と id_rsa.pub の２つの鍵が生成されます。

次に公開鍵を GitHub にアップします。

[ssh の設定画面](https://github.com/settings/ssh)から公開鍵の設定ができます。

開いたら画面右上の「New SSH key」を押します。  
「title」に公開鍵名(自分の名前とかなんでも)、「key」に公開鍵の中身を入れます。  
公開鍵の中身については、以下の操作をします。

```bash
$ cat id_rsa.pub
```

これを実行すると公開鍵の中身が出力されるので、内容をすべてコピーします。  
コピーが完了したら「key」の欄に貼り付けし(この時スペースなどが入っていないことに注意)、「Add key」を押すとパスワードを求められるので入力します。

接続が完了したか確かめます。以下のコマンドを入力します。

```bash
$ ssh -T git@github.com
```

そして「Hi (account 名)! You've successfully authenticated, but GitHub does not provide shell access.」と返ってきたら接続完了です。
