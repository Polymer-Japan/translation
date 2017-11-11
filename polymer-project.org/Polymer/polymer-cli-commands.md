## Polymer CLI コマンド

> This section explains various useful Polymer CLI commands that you'll want to incorporate into your development workflow while you build your element or app project.

ここでは、エレメントまたはアプリケーションを構築する際に、開発に役立つPolymer CLIコマンドについて説明します。

> The commands are intended for both element and app projects unless otherwise noted.

コマンドは、特に明記しない限り、エレメントとアプリケーションの両方を対象としています。

polymer build (プロジェクトのみ)
polymer init
polymer install
polymer lint
polymer serve
polymer test
Global options for Polymer CLI commands

### polymer build

> This command is for app projects only.

_このコマンドはアプリケーションのみを対象としております_

> Generates a production-ready build of your app.

プロダクション対応のアプリケーションを生成します。
 
> This process includes minifying the HTML, CSS, and JS of the application dependencies, 
> and generating a service worker to pre-cache dependencies.

このプロセスでは、アプリケーションのHTML、CSS、JSを縮小し、依存関係をキャッシュするサービスワーカーを生成します。

> Polymer CLI's build process is designed for apps that follow the PRPL pattern.
  
Polymer CLIのビルドプロセスは、PRPLパターンに沿ってアプリケーションを設計しています。

> To make sure your app builds properly, create a polymer.json file at the top-level of your project and store your build configurations there. 

アプリケーションが適切にビルドされていることを確認するには、プロジェクトの先頭にpolymer.jsonファイルを作成し、そこにビルド設定を保存します。

> See the polymer.json specification for more information.

詳細については、[polymer.jsonの仕様](https://www.polymer-project.org/2.0/docs/tools/polymer-json)を参照してください



> You can also pass equivalent values via the following command-line flags. 

次のcommand-lineフラグを使用して同等の値を渡すこともできます。

> This can be useful for building simple projects on your machine but you will need to include the flag every time you run the command.

これはシンプルなプロジェクトを構築するのに便利ですが、コマンドを実行するたびにフラグを含める必要があります。
 
> For most projects a polymer.json configuration file will be easier to work with and share across your team.

多くのプロジェクトでは、polymer.jsonを作成することで設定を共有しやすくなります。

- --add-service-worker
- --bundle
- --css-minify
- --entrypoint
- --html-minify
- --insert-prefetch-links
- --js-compile
- --js-minify
- --shell
- --fragment

> A set of presets have been provided to cover common configurations - see the section below on build presets.

共通の設定をカバーするプリセットが用意されています。以下のビルドプリセットのセクションを参照してください。


#### --add-service-worker

> Generate a service worker for your application to cache all files and assets on the client.

アプリケーションのすべてのファイルをキャッシュするサービスワーカーを生成します。

> Polymer CLI will generate a service worker for your build using the sw-precache library.

Polymer CLIは、[sw-precache](https://github.com/GoogleChrome/sw-precache)ライブラリを使用してビルド用のサービスワーカーを生成します。

> To customize your service worker, create a `sw-precache-config.js` file in your project directory that exports your configuration. 

サービスワーカーに変更を加えるには、プロジェクトディレクトリにsw-precache-config.jsファイルを作成します。

> See the sw-precache README for a list of all supported options.

サポートされているオプションについては、sw-precacheの[README](https://github.com/GoogleChrome/sw-precache)を参照してください。


> Note that the sw-precache library uses a cache-first strategy for maximum speed and makes some other assumptions about how your service worker should behave. 

sw-precacheライブラリは、高速化のために[cache-first](http://jakearchibald.com/2014/offline-cookbook/#cache-falling-back-to-network)を使用します。サービスワーカーに他の用途を持たせる場合に注意してください。

> Read the "Considerations" section of the sw-precache README to make sure that this is suitable for your application.

このオプションがアプリケーションに適していることを確認するには、sw-precache READMEの [Considerationsセクション](https://github.com/GoogleChrome/sw-precache#considerations)を読んでください。


#### --bundle

> By default, fragments are unbundled.

デフォルトでは、フラグメントはバンドルされていません。
 
> This is optimal for HTTP/2-compatible servers and clients.

これは、HTTP/2互換のサーバーとクライアントに最適です。

> If the --bundle flag is supplied, all fragments are bundled together to reduce the number of file requests. 

--bundleフラグを指定すると、すべてのフラグメントがバンドルされ、ファイルリクエストの数が削減されます。

> This is optimal for sending to clients or serving from servers that are not HTTP/2 compatible.

これは、クライアントへの送信やHTTP/2と互換性のないサーバーからの配信に最適です。


#### --css-minify

> Minify inlined and external CSS.

インラインCSS含め、CSSを縮小します。


#### --entrypoint

> A filename. 

ファイル名を指定します

> This is the main entrypoint into your application for all routes.

ここで指定したファイルがアプリケーションのエントリポイントになります。
 
> Often times this is your index.html file. 

デフォルトは`index.html`になっています。

> This file should import the app shell file specified in the shell option.

このファイルは、シェルオプションで指定されたアプリケーション[シェル](https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands#shell)ファイルをインポートする必要があります。

> It should be minimal since it's loaded and cached for each route.

また、ルートごとに読み込まれキャッシュされるため、ファイルサイズを最小限に抑える必要があります。


#### --html-minify

> Minify HTMl by removing comments and whitespace.
  
コメントと空白を削除してHTMlを縮小します。


#### --insert-prefetch-links

> Insert prefetch link elements into your fragments so that all dependencies are prefetched immediately.

すべての依存関係がすぐにプリフェッチされるように、プリフェッチリンクエレメントをフラグメントに挿入します。
 
> Add dependency prefetching by inserting <link rel="prefetch"> tags into entrypoint and <link rel="import"> tags into fragments and shell for all dependencies.
  
`<link rel="prefetch">`タグをエントリポイントに挿入し、`<link rel="import">`タグをすべての依存関係のフラグメントとシェルに挿入して、依存関係のプリフェッチを追加します。

#### --js-compile

> Use babel to compile all ES6 JS down to ES5 for older browsers.
  
古いブラウザ向けに、ES6をES5にコンパイルする`babel`を使います。

#### --js-minify

> Minify inlined and external JavaScript.

インラインJavaScriptと外部JavaScriptを縮小します。

#### --shell

> The app shell file containing common code for the app.

アプリの共通コードを含むアプリケーションシェルファイルを指定します。


#### --fragment

> This flag supports dynamic dependencies. 

このフラグは動的依存関係をサポートします。

> It is an array of any HTML filenames that are not statically linked from the app shell (that is, imports loaded on demand by importHref).
  
これは、アプリケーションシェルから静的にリンクされていない、HTMLファイル名の入った配列です。（つまり、`importHref`より必要に応じて読み込まれたものでえす）


> If a fragment has static dependencies, provided the fragment is defined in this property, the Polymer build analyzer will find them.

フラグメントに静的な依存関係がある場合、フラグメントがこのプロパティで定義されている場合は、Polymerビルドアナライザがそれらを検出します。

> You only need to list the file imported by importHref.

importHrefでインポートされたファイルをリストするだけです。



> In a Polymer app, 

Polymer アプリケーションでは

> the files listed in the fragments flag usually contain one or more element definitions that may or may not be required during the user’s interaction with the app, and can thus be lazily loaded.

フラグメントフラグに羅列されているファイルには、通常、ユーザがアプリケーションとやりとりしている間に必要となるかもしれない要素定義が含まれていて、遅延ロードすることができます。

#### プリセットを作成する

```
polymer build --preset preset-name
```

> Build presets provide an easy way to create common build configurations. 

ビルドプリセットは、共通のビルド構成を簡単に作成する方法を提供します。

> When you provide a valid preset for your build, it will use the flags in that preset. 

ビルドに有効なプリセットを指定すると、そのプリセットのフラグが使用されます。

> We currently support 3 different presets:

現在、3種類のプリセットをサポートしています

#### 例

> Create a bundled build for browsers that support ES5:

ES5をサポートするブラウザのバンドルビルドを作成します。

> Create an unbundled build for browsers that support ES6

ES6をサポートするブラウザのバンドルしないビルドを作成します。
