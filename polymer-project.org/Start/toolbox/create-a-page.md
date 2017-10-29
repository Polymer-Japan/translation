---
title: Step 2. Create a new page
subtitle: "Build an app with App Toolbox"
---

<!-- toc -->

`starter-kit` には、アプリケーションのビューを構築するためのプレースホルダーページが含まれています。
しかし、ある時点で、おそらくより多くのページを追加したくなるでしょう。

この手順では、アプリケーションに新しいページすなわちトップレベルビューを追加するプロセスを順を追って説明していきます。

## 新しいページ用の要素を作成

まず、新たなビューの内容をカプセル化する新しいカスタム要素を作成します。

1.  `src/my-new-view.html` という名前の新しいファイルを作成し、エディタで開きます。

2.  足場（scaffolding）となるコードを追加します。これらは、Polymerを用いた新しいカスタム要素定義のための足場となります：

    ```html
    <!-- Polymer.Element 基底クラスをロード -->
    <link rel="import" href="../bower_components/polymer/polymer-element.html">

    <dom-module id="my-new-view">
      <!-- Defines the element's style and local DOM -->
      <template>
        <style>
          :host {
            display: block;

            padding: 16px;
          }
        </style>

        <h1>New view</h1>
      </template>
      <script>
        // Your new element extends the Polymer.Element base class
        class MyNewView extends Polymer.Element {
          static get is() { return 'my-new-view'; }
        }
        //Now, register your new custom element so the browser can use it
        customElements.define(MyNewView.is, MyNewView);
      </script>
    </dom-module>
    ```

現時点では、要素はただ「New view」と記載のある`<h1>`があるだけのベーシックな状態ですが、
後で、もっと興味深いものにすることができます。

## アプリケーションへの要素の追加

カスタム要素は定義されましたが、まだアプリケーションによって使用されていません。
要素を使用するためには、アプリケーション側のHTMLに追加する必要がります。

1.  テキストエディタで `src/my-app.html` を開きます。

1.  `<iron-pages>` 要素内に既存ページ一式を見つける事ができます:

    ```
    <iron-pages
        selected="[[page]]"
        attr-for-selected="name"
        fallback-selection="view404"
        role="main">
      <my-view1 name="view1"></my-view1>
      <my-view2 name="view2"></my-view2>
      <my-view3 name="view3"></my-view3>
      <my-view404 name="view404"></my-view404>
    </iron-pages>
    ```

    `<iron-pages>` は、ルートと共に変化する` ページ` 変数にバインドされ、他のページを隠しながらアクティブなページを選択します。

1.  iron-pages タグ内に新しいページ要素を追加します:

    ```
    <my-new-view name="new-view"></my-new-view>
    ```

    `<iron-pages>` は次のようになります:

    ```
    <iron-pages
        selected="[[page]]"
        attr-for-selected="name"
        fallback-selection="view404"
        role="main">
      <my-view1 name="view1"></my-view1>
      <my-view2 name="view2"></my-view2>
      <my-view3 name="view3"></my-view3>
      <my-new-view name="new-view"></my-new-view>
      <my-view404 name="view404"></my-view404>
    </iron-pages>
    ```

    注：通常、新しいカスタム要素を追加する際は、コンポーネント定義の読み込みのため、HTML Import（訳者注：<link rel = "import">）を追加したくなるかもしれません。しかしながら、本アプリケーションテンプレートは、ルートに基いたトップレベルのビューを、必要に応じて遅延ロードするように予めセットアップされています。よって、今回のケースでは、新しい `<my-new-view>` 要素を使用するために、HTML Importを追加する必要はありません。
    
    アプリケーションテンプレートに付随する次のコードによって、ルートが変更された際に、各ページ定義が読みこまれていることが保証されます。
    ご覧のように、各ルートの定義をインポートする際、アプリケーションは単純な規約 (`'my-' + page + '.html'`) に従います。
    さらに複雑なルーティングと遅延ロードを処理するために、このコードを好きなように作り変えることができます。

    既存のテンプレートコード ー これを追記する必要はありません { .caption }

    ```
      _pageChanged(page) {
        // Load page import on demand. Show 404 page if fails
        var resolvedPageUrl = this.resolveUrl('my-' + page + '.html');
        Polymer.importHref(
            resolvedPageUrl,
            null,
            this._showPage404.bind(this),
            true);
      }
    ```

## ナビゲーションメニュー項目の作成

アプリケーション内に新しい要素定義と宣言を行いました。あとは、ユーザーが新しいページに移動できるように、左側のドロワーナビゲーションメニューに項目を追加するだけです。

1.  `src/my-app.html` をエディタで開いたままにしておいてください。

1.  `<app-drawer>` 要素内に、ナビゲーションメニューを見つけることができます。

    ```
      <!-- Drawer content -->
      <app-drawer id="drawer" slot="drawer">
        <app-toolbar>Menu</app-toolbar>
        <iron-selector selected="[[page]]" attr-for-selected="name" class="drawer-list" role="navigation">
          <a name="view1" href="/view1">View One</a>
          <a name="view2" href="/view2">View Two</a>
          <a name="view3" href="/view3">View Three</a>
        </iron-selector>
      </app-drawer>
    ```

    各ナビゲーションメニュー項目は、CSSでスタイル付けされたアンカー要素（`<a>`）で構成されています。

1.  次の新しいナビゲーション項目をメニューの下部に追加します。

    ```
    <a name="new-view" href="/new-view">New View</a>
    ```

    ナビゲーションメニューは次のようになります：

    ```
    ...
      <!-- Drawer content -->
      <app-drawer id="drawer" slot="drawer">
        <app-toolbar>Menu</app-toolbar>
        <iron-selector selected="[[page]]" attr-for-selected="name" class="drawer-list" role="navigation">
          <a name="view1" href="/view1">View One</a>
          <a name="view2" href="/view2">View Two</a>
          <a name="view3" href="/view3">View Three</a>
          <a name="new-view" href="/new-view">New View</a>
        </iron-selector>
      </app-drawer>
    ...
    ```

新しいページが完成しました！ `polymer serve --open` コマンドを使って、アプリケーションをローカルサーバーで確認してみましょう。

![Example new page](/images/2.0/toolbox/new-view.png)

## ビルドのためのページ登録

アプリケーションをWebにデプロイする際は、デプロイ用ファイルを準備するためにPolymer CLIを使用します。 Polymer CLIは、遅延ロードビューのような、要求に応じてロードされることになるフラグメント（HTMLコードの断片）について把握しておく必要があります。

1.  `polymer.json` をテキストエディタで開きます。

1.  `fragments` のリストに、`src/my-new-view.html` を追加します。

    新しいリストは次のようになります:

    ```
    "fragments": [
      "src/my-view1.html",
      "src/my-view2.html",
      "src/my-view3.html",
      "src/my-new-view.html",
      "src/my-view404.html"
    ]
    ```

注:  遅延ロードをさせたり、 `async` 属性を使って非同期でロードさせたりするファイルについては、`fragments` リストにファイル名を追加するだけで済みます。 同期読み込みとなる `<link rel = "import">` タグを使用してインポートされたファイルは、 `fragments` に追加*しないで*ください。

## 次のステップ

アプリケーションに新しいページを追加しました。次のステップでは、すぐに使える既製のカスタム要素をインストールしてアプリに追加する方法を学びます。

<a class="blue-button"
    href="add-elements">Next step: Add an element</a>
