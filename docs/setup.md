# 事前準備

## 【目次】

1. [はじめに](#はじめに)
2. [GitHub のアカウント登録](#github-のアカウント登録)
3. [Git のインストール](#git-のインストール)
4. [Git 構成ファイルのセットアップ](#git-構成ファイルのセットアップ)
5. [HTTPS, SSH 接続](#https-ssh-接続)
6. [HTTPS 接続の設定](#https-接続の設定)
7. [SSH 接続の設定](#ssh-接続の設定)
8. [さいごに](#さいごに)

## 【はじめに】

## 【GitHub のアカウント登録】

まずは、[GitHub](https://github.com)にアクセスします。  
ユーザーネーム、メールアドレス、パスワードなどの必要事項を入力し、アカウントを作成します。

https://github.com/[自分のユーザーネーム]
へアクセスして以下の画像のように自身のページが表示されたら完了です！

<img width="600" alt="スクリーンショット 2022-11-28 17 06 38" src="https://user-images.githubusercontent.com/50654077/204229886-41a87717-e4ca-407c-a095-6f1970f479d1.png">

(表示はいじっているので少し違います)

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
$ git --version
```

ex.)  
<img width="300" alt="スクリーンショット 2022-11-28 12 41 48" src="https://user-images.githubusercontent.com/50654077/204230307-3309499a-2a34-48b3-929f-5edde59e68a6.png">

## 【Git 構成ファイルのセットアップ】

### 【GitHub アカウントの登録】

先ほど作成した GitHub のアカウントと Git を紐付けます！  
以下のコマンドを実行してください。
([]で書かれている部分を自身の情報に修正してから実行してください。)

```bash
$ git config --global user.name [設定したユーザーネーム]
$ git config --global user.email [設定したメールアドレス]
```

以下のコマンドを実行して正しく設定されているか確認できれば OK です！

```bash
$ cat ~/.gitconfig
----------------------------------------
[user]
    name = take-cantik
    email = take.cantik17@gmail.com
```

### 【Git のエディタを変更する】

これはやってもやらなくてもいいものなので、本人にお任せします！

コミットログを書くときに Ubuntu のデフォルトだと nano に設定されてしまうので、これを Vim に修正します。  
(Vim なのは個人的に好きなだけなので、別のものでも構いません)

以下のコマンドを実行します。

```bash
$ git config --global core.editor 'vim -c "set fenc=utf-8"'
```

## 【HTTPS, SSH 接続】

GitHub 上のリモートリポジトリに接続するときに、通常 HTTPS と SSH の２種類の接続方法があります。

GitHub 公式では HTTPS を推奨しています。  
それぞれの違いとしては以下の通りです。

### HTTPS 接続

- GitHub の公式が推奨している
- ユーザーネーム、個人アクセストークンのみで認証できるので、どのデバイスからでもアクセスが可能
- HTTPS はすべてのファイアウォールで開かれている
- 毎回認証が必要(キャッシュを使えばその限りではない)

### SSH 接続

- 暗号化通信のため情報が漏れない
- 初回設定が面倒だが、毎度の認証が不要
- デバイス内のアクセス可能な場所に鍵のファイルが保存される
- 鍵が存在するデバイスでしかアクセスができない

個人的には SSH 推しですが、基本的にはどちらでも構いませんし(多分)、  
私は、デバイスなどにによって変えています。

どちらかを選んで以下の手順で設定してください！

## 【HTTPS 接続の設定】

2020 年 7 月に GitHub 公式が認証の際にパスワードではなく、個人アクセストークンを使用するということになりました。

ここでは、個人アクセストークンの発行方法、トークンをメモリに保存する方法を説明していきます。

まずは、個人アクセストークンを発行します。  
[設定の Developer settings のタブ](https://github.com/settings/apps)へアクセスします。

「Personal access tokens」のタブ(1)から「Tokens」を選択し(2)、  
「Generate new token」(3)から「Generate new token (classic)」を選択します。(4)

<img width="600" alt="スクリーンショット 2022-11-29 13 37 26" src="https://user-images.githubusercontent.com/50654077/209042891-ed697489-3ec4-4de6-9617-2d4c96159ea4.png">


フォームに必要な情報を入力していきます。

1. Note にはこのトークンが何のためのものかを入力します。  
   "HTTPS 接続用" とかで大丈夫です。
2. Expiration にはトークンの有効期限を設定します。  
   セキュリティの問題がありますので無期限にするのはお勧めしません。
3. Select scopes ではトークンのアクセス権限を設定します。
   今回は「repo」にチェックが入っていれば OK です。

<img width="600" alt="スクリーンショット 2022-11-29 13 46 59" src="https://user-images.githubusercontent.com/50654077/204448056-3113ed1c-ec9d-444c-a687-0808746d8b21.png">

ここまで入力が終わったら一番下の「Generate token」を押してトークンを作成します。

<img width="600" alt="スクリーンショット 2022-11-29 13 56 37" src="https://user-images.githubusercontent.com/50654077/204448093-ae584bf6-7883-488f-a846-4b2531950bcf.png">

確定すると、以下の画像のようにトークンが表示されます。  
このトークンは画面を移動すると二度と見れなくなるので、このタイミングで必ず保管しておきます。

<img width="600" alt="スクリーンショット 2022-11-29 13 56 56" src="https://user-images.githubusercontent.com/50654077/204448125-e62b05db-ae44-4be3-b2ea-cbee344b4c48.png">

以降はリモートリポジトリとの通信の際にパスワードを求められたら、この個人アクセストークンを使用します。

しかし、毎回毎回このトークンを入力するのはとても手間なので、  
`credential.helper` という認証情報を記録する仕組みを使って入力を省くことができます。

やり方は以下のコマンドを実行するだけです。

```bash
$ git config --global credential.helper 'cache --timeout=2592000'
```

※今回はトークンの有効期限を 30 日にしたので、2592000 秒に設定しています。(timeout オプションはなくてもいいです)

これで完了です！

## 【SSH 接続の設定】

これを行うと、リモートリポジトリとの通信の時に**パスワード入力する手間が省けます**。  
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

<img width="600" alt="スクリーンショット 2022-11-28 17 34 25" src="https://user-images.githubusercontent.com/50654077/204231215-adebc425-08a2-4ada-a07a-ff20dad036a0.png">

「title」に公開鍵名、「key」に公開鍵の中身を入れます。  
公開鍵の中身については、以下のコマンドで確認することができます。

```bash
$ cat id_rsa.pub
```

これを実行すると公開鍵の中身が出力されるので、内容をすべてコピーします。  
コピーが完了したら「key」の欄に貼り付けし(この時スペースなどが入っていないことに注意)、「Add key」を押すとパスワードを求められるので入力します。

<img width="600" alt="スクリーンショット 2022-11-29 14 42 08" src="https://user-images.githubusercontent.com/50654077/204448499-16704da6-ce6d-413d-82ce-a0ea443fa2d3.png">

接続が完了したか確かめます。以下のコマンドを入力します。

```bash
$ ssh -T git@github.com
```

そして「Hi (ユーザーネーム)! You've successfully authenticated, but GitHub does not provide shell access.」と返ってきたら接続完了です。

## 【さいごに】

ここまで済んだら準備は万端です！  
お疲れ様でした！

[こちら](words.md)に講義でよく使う用語の意味をまとめたので、こちらも合わせて見ておくとよりスムーズに進むと思います！  
全て理解できなくても全然 OK です！
