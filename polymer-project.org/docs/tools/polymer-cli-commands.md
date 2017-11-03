---
title: Polymer CLI コマンド
---

<!-- toc -->

ここでは、エレメントまたはアプリケーションを構築する際に、開発に役立つPolymer CLIコマンドについて説明します。

コマンドは、特に明記しない限り、エレメントとアプリケーションの両方を対象としています。

* [polymer build (プロジェクトのみ)](#build)
* [polymer init](#init)
* [polymer install](#install)
* [polymer lint](#lint)
* [polymer serve](#serve)
* [polymer test](#tests)
* [Global options for Polymer CLI commands](#global)

## polymer build {#build}

*このコマンドはアプリケーションのみを対象としております。*

プロダクション対応のアプリケーションを生成します。このプロセスでは、アプリケーションのHTML、CSS、JSを縮小し、依存関係をキャッシュするサービスワーカーを生成します。

Polymer CLIのビルドプロセスは、[PRPLパターン](/{{{polymer_version_dir}}}/toolbox/prpl)に沿ってアプリケーションを設計しています。

アプリケーションが適切にビルドされていることを確認するには、プロジェクトの先頭に`polymer.json`ファイルを作成し、そこにビルド設定を保存します。詳細については、[polymer.jsonの仕様](https://www.polymer-project.org/2.0/docs/tools/polymer-json)を参照してください。

次のcommand-lineフラグを使用して同等の値を渡すこともできます。これはシンプルなプロジェクトを構築するのに便利ですが、コマンドを実行するたびにフラグを含める必要があります。 多くのプロジェクトでは、`polymer.json`を作成することで設定を共有しやすくなります。

* [--add-service-worker](#service-workers)
* [--bundle](#bundles)
* [--css-minify](#css-minify)
* [--entrypoint](#entrypoint)
* [--html-minify](#html-minify)
* [--insert-prefetch-links](#prefetch)
* [--js-compile](#js-compile)
* [--js-minify](#js-minify)
* [--shell](#shell)
* [--fragment](#fragment)

共通の設定をカバーするプリセットが用意されています。以下の[ビルドプリセット](#presets)のセクションを参照してください。

### --add-service-worker {#service-workers}

アプリケーションのすべてのファイルをキャッシュするサービスワーカーを生成します。

Polymer CLIは、[sw-precache](https://github.com/GoogleChrome/sw-precache)ライブラリを使用してビルド用のサービスワーカーを生成します。サービスワーカーに変更を加えるには、プロジェクトディレクトリに`sw-precache-config.js`ファイルを作成します。サポートされているオプションについては、sw-precacheの[README](https://github.com/GoogleChrome/sw-precache)を参照してください。

sw-precacheライブラリは、高速化のために[cache-first](http://jakearchibald.com/2014/offline-cookbook/#cache-falling-back-to-network)を使用します。サービスワーカーに他の用途を持たせる場合に注意してください。このオプションがアプリケーションに適していることを確認するには、sw-precache READMEの [Considerationsセクション](https://github.com/GoogleChrome/sw-precache#considerations)を読んでください。

### --bundle {#bundles}

デフォルトでは、フラグメントはバンドルされていません。これは、HTTP/2互換のサーバーとクライアントに最適です。

`--bundle`フラグを指定すると、すべてのフラグメントがバンドルされ、ファイルリクエストの数が削減されます。これは、クライアントへの送信やHTTP/2と互換性のないサーバーからの配信に最適です。

### --css-minify {#css-minify}

インラインCSS含め、CSSを縮小します。

### --entrypoint {#entrypoint}

ファイル名を指定します。ここで指定したファイルがアプリケーションのエントリポイントになります。デフォルトは`index.html`になっています。このファイルは、シェルオプションで指定されたアプリケーション[シェル](https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands#shell)ファイルをインポートする必要があります。また、ルートごとに読み込まれキャッシュされるため、ファイルサイズを最小限に抑える必要があります。

### --html-minify {#html-minify}

コメントと空白を削除してHTMlを縮小します。

### --insert-prefetch-links {#prefetch}
すべての依存関係がすぐにプリフェッチされるように、プリフェッチリンクエレメントをフラグメントに挿入します。`<link rel="prefetch">`タグをエントリポイントに挿入し、`<link rel="import">`タグをすべての依存関係のフラグメントとシェルに挿入して、依存関係のプリフェッチを追加します。

### --js-compile {#js-compile}

Use babel to compile all ES6 JS down to ES5 for older browsers.

### --js-minify {#js-minify}

Minify inlined and external JavaScript.

### --shell {#shell}

The app shell file containing common code for the app.

### --fragment {#fragment}

This flag supports dynamic dependencies. It is an array of any HTML filenames that are not
statically linked from the app shell (that is, imports loaded on demand by `importHref`).

If a fragment has static dependencies, provided the fragment is defined in this property, the
Polymer build analyzer will find them. You only need to list the file imported by importHref.

In a Polymer app, the files listed in the fragments flag usually contain one or more element
definitions that may or may not be required during the user’s interaction with the app, and can
thus be lazily loaded.

### Build presets {#presets}

```bash
polymer build --preset preset-name
```

**Build presets** provide an easy way to create common build configurations. When you provide a valid preset for your build, it will use the flags in that preset. We currently support 3 different presets:

- **es5-bundled:**
  --js-minify --js-compile --css-minify --bundled --add-service-worker --add-push-manifest --insert-prefetch-links

- **es6-bundled:**
  --js-minify --css-minify --html-minify --bundled --add-service-worker --add-push-manifest --insert-prefetch-links
  
- **es6-unbundled:**
  --js-minify --css-minify --html-minify --add-service-worker --add-push-manifest --insert-prefetch-links

### Examples {#examples}

Create a bundled build for browsers that support ES5:

`polymer build --preset es5-bundled`

Create an unbundled build for browsers that support ES6:

`polymer build --preset es6-unbundled`

## polymer init {#init}

Initializes a Polymer project from one of several templates. Pre-bundled templates range from just bare-bones to fully featured applications like the [Polymer Shop app](/{{{polymer_version_dir}}}/toolbox/case-study).

Run `polymer init` to choose a template from a list of all installed templates. Or, if you know the template name before hand, you can provide it as a command argument to select it automatically.

See the [polymer-cli readme](https://github.com/Polymer/polymer-cli#polymer-init-template) for more information on the `polymer init` command. 

See also:

* [Create an element project with the Polymer CLI](create-element-polymer-cli)
* [Create an application project with the Polymer CLI](create-app-polymer-cli)
* [Case study of the Polymer Shop app](/{{{polymer_version_dir}}}/toolbox/case-study)

## polymer install {#install}

Installs Bower dependencies. Running `polymer install` is equivalent to running `bower install`.

The `--variants` flag allows you to install dependency variants. See the documentation on [managing dependencies for hybrid elements](/{{{polymer_version_dir}}}/docs/devguide/hybrid-elements#dependency-variants) for more information.

The `--offline` flag tells the install command not to hit the network to retrieve components. If components are not cached, the install will fail.

## polymer lint {#lint}

Analyze your project for syntax errors, missing imports, bad databinding expressions and more. `polymer lint` helps with identifying issues across your HTML, JS, and CSS based on an in-depth analysis of web components in source code. It does not reinvent the wheel though, it focuses on issues specific to web components and Polymer, so it is a good adjunct to other tools like [`eslint`](http://eslint.org/) and [`htmlhint`](http://htmlhint.com/).

Use it like so:

    polymer lint --rules=polymer-2

This will lint all of the code in your project with the `polymer-2` ruleset, which is appropriate for projects using Polymer 2.0. If your code is hybrid and should work with either Polymer 1.x or 2.x then `polymer-2-hybrid` is a better choice, as it will warn you about use of features that do not exist in Polymer 2.x.

You can pass flags to the linter like `--rules` but even better is to put the configuration in `polymer.json` so that all you need to do is run `polymer lint`. Putting your configuration in `polymer.json` also means that other tools, like IDE plugins can use the same lint configuration.

Here's what that looks like:

```json
{
  "lint": {
      "rules": ["polymer-2"],
      "ignoreWarnings": []
  }
}
```

- `rules`: An array of lint rules and rule collections to run on your project. For most projects, one of  `polymer-2`, `polymer-2-hybrid`, or `polymer-1` is all that's needed here.
- `ignoreWarnings`: An array of warning codes to ignore.

### Warning Codes:

The output of `polymer lint` looks like this:

```
            <iron-collapse>
            ~~~~~~~~~~~~~~~

index.html(83,12) warning [undefined-elements] - The element iron-collapse is not defined
```

This means that on line 83 of `index.html` there's an `<iron-collapse>` tag, but the linter can't find the definition of the `iron-collapse` custom element. This probably means that there's a missing HTML import in `index.html`. To ignore this warning, add `undefined-elements` to the `ignoreWarnings` array in `polymer.json`.

## polymer serve {#serve}

Runs a local web server.

If you want to view a live demo of your element or app, run the local web server:

    polymer serve

To view the demo, point your browser to one of the following URLs.

Element project demo:

<pre><code>http://localhost:8080/components/<var>my-el</var>/demo/</code></pre>

Element project API reference:

<pre><code>localhost:8080/components/<var>my-el</var>/</code></pre>

App project demo:

    http://localhost:8080

### Server options {#server-options}

This section shows examples of using various `polymer serve` options.

Serve from port 3000:

    polymer serve --port 3000

If you have configured a custom hostname on your machine, Polymer CLI can serve it with the
`--hostname` argument (for example, app project demo is available at `http://test:8080`):

    polymer serve --hostname test

Open up a page other than the default `index.html` in a specific browser
(Apple Safari, in this case):

    polymer serve --open app.html --browser Safari

## polymer test {#tests}

Runs tests.

If you want to run tests on your element or app project, `cd` to the base directory of your project
and run:

    polymer test

Polymer CLI automatically runs all of the tests that it finds in the `test` directory. You'll see
the results of the tests in your CLI.

If you create your own tests, they should also go in the `test` directory.

The underlying library that powers `polymer test` is called `web-component-tester` (`wct`). Learn
more about creating unit tests with `wct`
in [Test your elements](tests).

## Global options for Polymer CLI commands {#global}

You can see a list of global options by running `polymer help`. Most of them
are self-explanatory.

The following commands are currently only supported for the `polymer build`
command, with planned support for other commands in the future.

*   `entry`
*   `shell`
*   `fragment`

See [`polymer build`](#build) for more information on how to use these options.
