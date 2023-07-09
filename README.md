# FANBOX-downloader beta
pixivFANBOXから画像や文章やファイルをダウンロードします。\
あくまで個人で楽しむために利用するものとし、**取得したデータを外部に公開するのは絶対におやめください**。

## とりあえず一通りは完成しました。
しかしまだベータ版とさせてください。
- 今後仕様を変更する可能性があります。
- まだ細かいオプションは一切搭載していません。
  - これから制作します。

## 使い方
### 準備
1. Python3.11.4以降をインストールする。

1. 以下のコマンドを実行しておく
```
python3.11 -m pip install -r requirements.txt
```

### 使い方
```
python3.11 main.py <クリエイターID>
```
クリエイターIDとはURLの以下の部分のこと
- `https://www.fanbox.cc/@<クリエイターID>/`
  - @を含めないように注意
- `https://<クリエイターID>.fanbox.cc/`

<br>

有料プランの投稿をダウンロードする時はセッションIDを使う。
```
python3 main.py -s <セッションID> <クリエイターID>
```
セッションIDはブラウザの通信から抜き取れる。
- セッションIDはログインしてからFANBOXのページを開くことで取得できる。
  - cookieのFANBOXSESSIDの値がセッションID
- `https://api.fanbox.cc/`との通信には大体入っている（はず）
  - わからなければ`post.listCreator`とかを確認してみよう。

cookieの中身を見れる拡張機能でも確認できるかも（未確認）


## 動作環境
- Python 3.11.4 以降

## Q & A
### Q. ダウンロードが遅い
A. 意図的にダウンロードを遅らせています。\
ソースコードを書き換えて速度を上げることは可能ですが、[pixivのサービス共通利用規約](https://policies.pixiv.net/)の第14条 第19項においてサービス側のサーバーに負荷をかけることは明確に禁止されていますので、自重してください。

### Q. ダウンロードしたファイルが細かくフォルダ分けされていて見づらい
A. 仕様です。

### Q. 取得できていない画像・ファイルがある
A. 支援者向けコンテンツの可能性があります。 \
ブラウザ上で支援した後、セッションIDを渡して再取得してください。


## ダウンロードしたファイルの構造

`/`
- `posts`
  - `<クリエイターID>`
    - `<投稿ID>`
      - `images`
        - 投稿内の画像
      - `files`
        - 投稿内のファイル
      - `post`
        - 投稿情報が入ったjson
      - `thumbnails`
        - サムネイル画像
    - `postlist`
      - 各種投稿の概要がまとめられているjson
- `profiles`
  - `<クリエイターID>`
    - `cover`
      - クリエイターページのカバー画像
    - `icon`
      - クリエイターのアイコン
    - `images`
      - プロフィールのポートフォリオ画像
    - `info`
      - クリエイター情報
    - `thumbnails`
      - ポートフォリオ画像のサムネイル
