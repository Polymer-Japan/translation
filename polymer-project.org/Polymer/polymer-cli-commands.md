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



