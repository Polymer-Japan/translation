---
title: Step 3. Add some elements
subtitle: "Build an app with App Toolbox"
---

<!-- toc -->

アプリケーションへの新規ビュー追加が済み、ビューの細かい箇所を構築するスタートラインに立ちました。

このプロセスでは、例えば [webcomponents.org][webcomponents.org] などの既成のコンポーネントを使用したいと思うかもしれません。

## 既成のコンポーネントのインストール

インストールしたいコンポーネントを特定したら、コンポーネントのbowerパッケージ名を探してください。

このステップでは、[webcomponents.org][paper-checkbox]に掲載されているPolymerの `<paper-checkbox>` 要素をアプリに追加します。
Bowerを使用してインストールすることができます。

プロジェクトのルートディレクトリから次のコマンドを実行してください:

    bower install --save PolymerElements/paper-checkbox

## アプリケーションへの要素追加

1.  テキストエディタで `src/my-new-view.html` を開きます。

1.  依存ファイルである `paper-checkbox.html` をimportします。

    既に記載のある `polymer-element.html` importの下に下記を追加します:

    ```
    <link rel="import" href="../bower_components/paper-checkbox/paper-checkbox.html">
    ```

1.  要素のテンプレートに `<paper-checkbox>` 要素を追加します。

    ```
    <paper-checkbox>Ready to deploy!</paper-checkbox>
    ```

    前の手順で追加した `<h1>` の下に追加します。新しいテンプレートは次のようになります:

    ```
    <!-- Defines the element's style and local DOM -->
    <template>
      <style>
        :host {
          display: block;

          padding: 16px;
        }
      </style>

      <h1>New view</h1>
      <paper-checkbox>Ready to deploy!</paper-checkbox>
    </template>
    ```

新しいビューの中で動作しているペーパーチェックボックスを見つけられるはずです：
You should be able to see the `paper-checkbox` working in your new view now:

![Example of page with checkbox](/images/2.0/toolbox/starter-kit-checkbox.png)

## 次のステップ

サードパーティコンポーネントをページに追加しました。次は、[Webへのアプリケーションのデプロイ](deploy)方法を学んでいきます。

[bower]: http://bower.io/
[webcomponents.org]: https://www.webcomponents.org
[paper-checkbox]: https://www.webcomponents.org/element/PolymerElements/paper-checkbox
