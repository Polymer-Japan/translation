# Polymer-Japan/translation

## 概要
このリポジトリはPolymer公式ドキュメント以外の翻訳を行うリポジトリです。  
公式ドキュメントは下記リポジトリで翻訳を行っています。  
[Polymer-Japan/docs](https://github.com/Polymer-Japan/docs)

## 翻訳対象
このリポジトリでは主に以下のようなウェブサイト、ドキュメントの翻訳を行います。

* [webcomponents.org](https://www.webcomponents.org/)
* [Web Fundamentals](https://developers.google.com/web/fundamentals/)
* [Code labs](https://codelabs.developers.google.com/)

### 翻訳対象リスト
https://docs.google.com/spreadsheets/d/1u5jd2pkTnWKkIeUtZa-3bu3hTYYrVY3oluzd_meDsBE/edit?usp=sharing

## 翻訳作業の流れ
翻訳作業は次のような流れで行います。

1. Projectで翻訳対象ページのカードを作業中に移動。カードがない場合はカードを作成しissue化する。
2. 作業ブランチをfeatureフォルダ配下に作成。名前はissueのIDとそろえる。（例：feature/#10）
3. コミットメッセージにはissueのIDを入れる。（例：「#10 誤字修正」）
4. 翻訳作業が終わったらPRを作成し、カードをレビュー中に移動する。
5. レビューが終わったらカードを「レビュー完了」に移動する。
6. デプロイ作業を行い、その後masterにマージする。その後、issueをクローズする。

わからないことがあればSlackで@Katsunori Tanakaか@takanori okiあてに質問してください。

## デプロイの方法
翻訳対象によって翻訳後のデプロイの仕方が異なります。注意してください。

### Web Fundamentals
[Web FundamentalsのGitHubリポジトリ](https://github.com/google/WebFundamentals)にPRを送ります。
下記ディレクトリに日本語のドキュメントのソースがあるので、ここに翻訳したものを追加してPR送ります。
[WebFundamentals/src/content/ja/fundamentals/](https://github.com/google/WebFundamentals/tree/master/src/content/ja/fundamentals)

### webcomponents.org, Code labs
これらは[Polymer Japanの公式サイト](https://polymer-jp.org/)で公開します。  
公式サイト上でページの編集ができるので、`@howking`さんに権限をもらうか、`@Katsunori Tanaka`か`@takanori oki`に依頼してください。  
どこにページを追加するかは検討中。

## 翻訳するときに注意すること
翻訳時に注意することは[Polymer-Japan/docsリポジトリのWiki](https://github.com/Polymer-Japan/docs/wiki/%E7%BF%BB%E8%A8%B3%E3%81%AE%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85)にまとまっているので、必ず確認、遵守してください。

## textlint
ローカルでtextlintを使用するには下記コマンドを実行してください。（node.jsがインストールされていることが前提です。）

```
yarn install
yarn textlint
```
