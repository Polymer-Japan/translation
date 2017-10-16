## Polymer CLI

> Polymer CLI is the official command line tool for Polymer projects and Web Components. 

Polymer CLIはPolymerプロジェクトとWebコンポーネント用の公式のコマンドラインツールです。

> It includes a build pipeline, a boilerplate generator for creating elements and apps, a linter, a development server, and a test runner.

ビルドパイプライン、カスタムエレメントとアプリケーションを作成するためのボイラープレート、リンター、開発サーバー、テストランナーが含まれています。


> Follow these instructions to install the Polymer CLI on a Linux or MacOS operating system.

Linuxまたは、MacOSオペレーティングシステムにPolymer CLIをインストールするには、以下の手順に従ってください。


> For a suggested way to run the Polymer CLI on Windows 10, see the instructions below on Installing Polymer CLI pre-requisites on Windows 10.

Windows 10でPolymer CLIを実行するための推奨方法については、下記の[Windows 10でのPolymer CLIのインストール](https://www.polymer-project.org/2.0/docs/tools/polymer-cli#windows-10)に関する説明を参照してください。



## Install Polymer CLI

> Make sure you have installed a version of Node.js supported by Polymer. To check the version of Node.js that you have installed, run:
  
- PolymerがサポートしているNode.jsのバージョンをインストールしていることを確認してください。インストールしたNode.jsのバージョンを確認するには、次のコマンドを実行します。

```
  node --version
```

> See the official node version support policy for more details.

詳細は[公式Nodeバージョンサポートポリシー](https://www.polymer-project.org/2.0/docs/tools/node-support)を参照してください。

> Update npm.

- npmをアップデートします

```
  npm install npm@latest -g
```

> Ensure that Git is installed.

- Gitがインストールされていることを確認してください。

```
git --version
```

> If it isn't, you can find it on the Git downloads page.

または、[Git downloads ページ](https://git-scm.com/downloads)で見つけることができます。


> Install the latest version of Bower.

- Bowerの最新バージョンをインストールします。

```
npm install -g bower
```

> Install Polymer CLI.

- Polymer CLIをインストールします

```
npm install -g polymer-cli
```

> Bower deprecation warning.In the output from this command, you may see an npm warning about Bower being deprecated. You can safely ignore this warning. See Bower.io for more information.

 **Bower deprecation warning**
 このコマンド出力はBowerの廃止予定に関するnpmの警告なのですが、この警告は無視しても問題ありません。詳細については、[Bower.io](https://bower.io/blog/)を参照してください。
 
  
> You're all set. Run polymer help to view a list of commands.

インストールは以上です。`polymer help`を実行して、コマンドのリストを表示してみましょう。