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

### polymer init

> Initializes a Polymer project from one of several templates.

いくつかのテンプレートの1つからPolymerプロジェクトを初期化します。

> Pre-bundled templates range from just bare-bones to fully featured applications like the Polymer Shop app.
  
用意されているテンプレートには、基本的なものから[Polymer Shopアプリ](https://www.polymer-project.org/2.0/toolbox/case-study)のような完全に機能するアプリケーションまで、色々のものがあります。



> Run polymer init to choose a template from a list of all installed templates. 

`polymer init`を実行しますと、インストールされているテンプレートの中からひとつを選択します。

> Or, if you know the template name before hand, you can provide it as a command argument to select it automatically.

または、テンプレート名がわかっている場合は、それをコマンド引数として指定することができます。

> See the polymer-cli readme for more information on the polymer init command.

`polymer init`コマンドの詳細については、[polymer-cli readme](https://github.com/Polymer/polymer-cli#polymer-init-template)を参照してください。

> See also

以下も参考にして下さい

> Create an element project with the Polymer CLI

[Polymer CLIを使用したエレメントプロジェクトの作成](https://www.polymer-project.org/2.0/docs/tools/create-element-polymer-cli)

> Create an application project with the Polymer CLI

[Polymer CLIを使用したアプリケーションプロジェクトの作成](https://www.polymer-project.org/2.0/docs/tools/create-app-polymer-cli)

> Case study of the Polymer Shop app

[Polymer Shopアプリのケーススタディ](https://www.polymer-project.org/2.0/toolbox/case-study)


### polymer install

> Installs Bower dependencies. Running polymer install is equivalent to running bower install.

Bowerよりインストールを行います。`polymer install`は、`bower install`と同じように動きます。

> The --variants flag allows you to install dependency variants. 

`--variants`フラグを使用すると、バージョン依存をインストール出来ます。

> See the documentation on managing dependencies for hybrid elements for more information.
  
詳細については、[ハイブリッドエレメントの依存関係の管理](https://www.polymer-project.org/2.0/docs/devguide/hybrid-elements#dependency-variants)に関するドキュメントを参照してください。


> The --offline flag tells the install command not to hit the network to retrieve components.

`--offline`フラグは、ネットワークからコンポーネントを取得させないようにします。
 
> If components are not cached, the install will fail.

これは、コンポーネントがキャッシュされていない場合には、インストールは失敗します。


### polymer lint

> Analyze your project for syntax errors, missing imports, bad databinding expressions and more. 

プロジェクトの構文、インポート、データバインディングなどにエラーが無いかをチェックします。

> polymer lint helps with identifying issues across your HTML, JS, and CSS based on an in-depth analysis of web components in source code.

`polymer lint`は、ソースコード内のWebコンポーネントの分析から、HTML、JS、およびCSSの問題を特定するのに役立ちます。
 
> It does not reinvent the wheel though, it focuses on issues specific to web components and Polymer, so it is a good adjunct to other tools like eslint and htmlhint.

`polymer lint`は、WebコンポーネントとPolymerに焦点を当てており、`eslint`や`htmlhint`のような他のlintツールのような機能は持っておりません。

> Use it like so:

使い方

```
 polymer lint --rules=polymer-2
```

> This will lint all of the code in your project with the polymer-2 ruleset, which is appropriate for projects using Polymer 2.0.

これにより、`polymer-2`のルールに適するように、プロジェクトをlintします。

> If your code is hybrid and should work with either Polymer 1.x or 2.x then polymer-2-hybrid is a better choice, as it will warn you about use of features that do not exist in Polymer 2.x.

コードがハイブリッドで、Polymer 1.x、または、2.xで動作する必要がある場合は、Polymer 2.xには存在しない機能を使用すると警告されますので、`polymer-2-hybrid`を選択することをお勧めします。


> You can pass flags to the linter like --rules but even better is to put the configuration in polymer.json so that all you need to do is run polymer lint. 

linterに`--rules`のようなフラグを渡すことはできますが、`polymer.json`に設定を書くことで`polymer int`のみで実行が可能になります。

> Putting your configuration in polymer.json also means that other tools, like IDE plugins can use the same lint configuration.
  
ここで設定した内容は、IDEプラグインのような、他のツールにも使うことができます。

> Here's what that looks like:

設定の例:

```
  "lint": {
      "rules": ["polymer-2"],
      "ignoreWarnings": []
  }
```

> rules: An array of lint rules and rule collections to run on your project.

rules: lintルールを設定する配列。
 
> For most projects, one of polymer-2, polymer-2-hybrid, or polymer-1 is all that's needed here.

多くのプロジェクトでは、`polymer-2`、`polymer-2-hybrid`、または`polymer-1`のいずれかが必要になります。


> ignoreWarnings: An array of warning codes to ignore.

ignoreWarnings: 無効にしたい警告を指定する配列になります。

#### Warning Codes:

> The output of polymer lint looks like this:

Warningが会った場合に、次のように表示されます

> This means that on line 83 of index.html there's an <iron-collapse> tag, but the linter can't find the definition of the iron-collapse custom element.

上記は、index.html 83行目に`<iron-collapse>`タグがありますが、`iron-collapse`カスタムエレメントを見つけることが出来ません。と表しております。
 
> This probably means that there's a missing HTML import in index.html. 

`index.html`のHTMLインポートが間違っていることが予想されます。

> To ignore this warning, add undefined-elements to the ignoreWarnings array in polymer.json.

この警告を無効にする場合は、`polymer.json`の`ignoreWarnings`配列に、`undefined-elements`を追加します。


### polymer serve

> Runs a local web server.
  
ローカル環境でウェブサーバーを立ち上げます。

> If you want to view a live demo of your element or app, run the local web server:
  
作ったアプリケーションのデモを確認したい場合に、ローカル環境のウェブサーバーで確認します。

```
polymer serve
```

> To view the demo, point your browser to one of the following URLs.
  
デモを表示するには、ブラウザで次のURLを指定します。

> Element project demo:

エレメントプロジェクトのデモの場合

> Element project API reference:

エレメントプロジェクトのAPIリファレンスの場合

> App project demo:

アプリケーションプロジェクトの場合


#### Server options

> This section shows examples of using various polymer serve options.
  
ここからは、`polymer serve`のオプションの使用例を見ていきましょう。

##### --port

> Serve from port 3000:

サーバーのポートを3000番に指定した場合。

##### --hostname

> If you have configured a custom hostname on your machine, Polymer CLI can serve it with the --hostname argument (for example, app project demo is available at http://test:8080):

ホスト名を独自に設定している場合は、`--hostname`引数から指定が行えます（例、appプロジェクトのデモでは、`http://test:8080`より利用できます）。

##### --open

> Open up a page other than the default index.html in a specific browser (Apple Safari, in this case):

特定のブラウザ（この場合は、Apple Safari）では、デフォルトページのindex.html以外のページを開きます。

##### --compile

> By default, the server will automatically use Babel to transpile any ES6 code down to ES5 for browsers that don't have native support for important ES6 features like classes.

通常は、class構文などのES6の機能をサポートしていないブラウザのために、Babelを使用して自動的にES5にトランスパイルしています。
 
> This behavior can be explicitly turned on or off for all browsers via the --compile option.
  
この動作は、--compileオプションを使用して、オンまたはオフにすることができます。

> Valid values are "auto", "always" and "never". 

設定値には "auto"、 "always"、 "never"があります。

> "auto" compiles JavaScript to ES5 for browsers that don't fully support ES6.

"auto"は、ES6に対応していないブラウザに対しては、JavaScriptをES5にコンパイルします。

> Always compile ES6 to ES5:

常にES6をES5にコンパイルする場合:

> Never compile ES6 to ES5:

ES6をES5にコンパイルしない場合:

> (Default) Automatically compile to ES5 for browsers that don't fully support ES6:
  
（デフォルト）ES6に対応していないブラウザの時に、自動的にコンパイルする場合:



> Automatic compilation can cause problems when running in device emulation mode on Chrome. 

autoの場合は、Chromeのデバイスエミュレーションモードで実行すると、問題を引き起こす場合があります。

> If the browser sends another browser's user-agent string, the server may switch between compiled and uncompiled responses, leaving the browser with an inconsistent set of resources in its cache.
 
ブラウザが別のブラウザのユーザエージェント文字列を送信すると、サーバはコンパイルされたレスポンスとコンパイルされていないレスポンスを切り替えて、キャッシュ内に一貫性のないリソースセットを残します。
 
> This issue may also occur in other browsers with device emulation capabilities. 

この問題は、デバイスエミュレーション機能を備えた他のブラウザでも発生する可能性があります。

> Use --compile always or --compile never to avoid this problem.

この問題を回避するには、--compile alwaysまたは--compile neverを使用してください。


> Run polymer help serve for the full list of available options.

使用可能なオプションについては、`polymer help serve`を実行してください。


### polymer test

> Runs tests.

テストを実行します

> If you want to run tests on your element or app project, cd to the base directory of your project and run:

エレメントやプロジェクトのテストを実行したい場合は、ルートディレクトリに移動して以下のコマンドを実行してください

```
polymer test
```

> Polymer CLI automatically runs all of the tests that it finds in the test directory.

Polymer CLIは、`test`ディレクトリで検出したすべてのテストを自動的に実行します。

> You'll see the results of the tests in your CLI.

テスト結果はCLIに表示されます。

> If you create your own tests, they should also go in the test directory.
  
独自のテストを作成する場合は、`test`ディレクトリに移動します。

> The underlying library that powers polymer test is called web-component-tester (wct). 

`polymer test`を実行する基礎となるライブラリは、`web-component-tester（wct）`と呼ばれます。

> Learn more about creating unit tests with wct in Test your elements.

`wct`を使ったユニットテストの作り方については[Test your elements](https://www.polymer-project.org/2.0/docs/tools/tests)をご覧ください


### Polymer CLI コマンドのグローバルオプション

> You can see a list of global options by running polymer help. Most of them are self-explanatory.

`polymer help`を実行すると、グローバルオプションのリストが表示されます。

> The following commands are currently only supported for the polymer build command, with planned support for other commands in the future.

次のコマンドは現在、`polymer build`コマンドでのみ使用できます。将来的には、他のコマンドでも使用できる予定になります。


> See polymer build for more information on how to use these options.

さらに詳しい情報を見たい方は、(polymer build)[https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands#build]でのオプションの項目をご覧ください。

