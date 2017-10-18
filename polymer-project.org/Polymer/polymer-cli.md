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


> CLI project types

## CLI project types

> Polymer CLI works with two types of projects:

Polymer CLIは2種類のプロジェクトで動作します。


> Elements projects. 

エレメントプロジェクト

> In an element project, you expose a single element or group of related elements which you intend to use in other element or app projects, or distribute on a registry like Bower or NPM.

エレメントプロジェクト, 他のエレメントプロジェクトやアプリプロジェクトで使用する単一エレメントまたは関連エレメントのグループを公開するか、BowerやNPMなどに配布します。
 
> Elements are reusable and organized to be used alongside other elements, so components are referenced outside the project.

エレメントは他のエレメントとともに使用するために再利用可能で構成されているため、コンポーネントはプロジェクトの外部で参照されます。



> See the guide to creating an element project with the Polymer CLI for more information.

詳細については、[Polymer CLIを使用したエレメントプロジェクトの作成](https://www.polymer-project.org/2.0/docs/tools/create-element-polymer-cli)に関するガイドを参照してください。



> Application projects. 

アプリケーションプロジェクト

> In an app project, you build an application, composed of Polymer elements, which you intend to deploy as a website.

アプリケーションプロジェクトでは、Polymerで構成されたアプリケーションを作成できます。このアプリケーションはWebサイトとして展開します。
 
> Applications are self-contained, organized with components inside the application.

アプリケーションは自己完結型で、アプリケーション内のコンポーネントで構成されています。



> See the guide to creating an application project with the Polymer CLI for more information.
  
詳細については、[Polymer CLIを使用してアプリケーションプロジェクトを作成する](https://www.polymer-project.org/2.0/docs/tools/create-app-polymer-cli)ためのガイドを参照してください。


## Commands

> See the documentation on Polymer CLI commands for a list of commands and how to use them.

コマンドとそれらの使用方法については、[Polymer CLI commands](https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands)を参照してください。


> Installing Polymer CLI pre-requisites on Windows 10

## Windows 10にPolymer CLIをインストールする前提条件

> There are multiple ways to install the pre-requisites for the Polymer CLI on a Windows 10 system.

Windows 10システムでPolymer CLIの前提条件をインストールするには、複数の方法があります。
 
> This method uses Bash on the Windows Subsystem for Linux.

ここでは、WindowsサブシステムのBashを使用します。



> For complete and up-to-date installation instructions for Bash on the Windows Subsystem for Linux, we recommend you review the Bash on ubuntu on Windows documentation.
  
Bashの最新のインストール手順については、[WindowsのUbuntuに関するドキュメント](https://msdn.microsoft.com/en-us/commandline/wsl/about)を参照してください。
