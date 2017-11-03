---
title: Polymer CLI
---

<!-- toc -->

Polymer CLIはPolymerプロジェクトとWebコンポーネント用の公式のコマンドラインツールです。ビルドパイプライン、カスタムエレメントとアプリケーションを作成するためのボイラープレート、リンター、開発サーバー、テストランナーが含まれています。

Linuxまたは、MacOSオペレーティングシステムにPolymer CLIをインストールするには、以下の手順に従ってください。

Windows 10でPolymer CLIを実行するための推奨方法については、下記の[Windows 10でのPolymer CLIのインストール](https://www.polymer-project.org/2.0/docs/tools/polymer-cli#windows-10)に関する説明を参照してください。

## Install Polymer CLI {#install}

1.  PolymerがサポートしているNode.jsのバージョンをインストールしていることを確認してください。インストールしたNode.jsのバージョンを確認するには、次のコマンドを実行します。
    
        node --version
    
    詳細は[公式Nodeバージョンサポートポリシー](https://www.polymer-project.org/2.0/docs/tools/node-support)を参照してください。

1.  npmをアップデートします

        npm install npm@latest -g

1.  Gitがインストールされていることを確認してください。

        git --version

    または、[Git downloads ページ](https://git-scm.com/downloads)で見つけることができます。

1.  Bowerの最新バージョンをインストールします。

        npm install -g bower

1.  Polymer CLIをインストールします。

        npm install -g polymer-cli

    **Bower deprecation warning:**  このコマンド出力はBowerの廃止予定に関するnpmの警告なのですが、この警告は無視しても問題ありません。詳細については、[Bower.io](https://bower.io/blog/)を参照してください。
    {.alert .alert-info}

インストールは以上です。`polymer help`を実行して、コマンドのリストを表示してみましょう。

## CLI project types {#project-types}

Polymer CLIは2種類のプロジェクトで動作します：

* エレメントプロジェクト。他のエレメントプロジェクトやアプリプロジェクトで使用する単一エレメントまたは関連エレメントのグループを公開するか、BowerやNPMなどに配布します。エレメントは他のエレメントとともに使用するために再利用可能で構成されているため、コンポーネントはプロジェクトの外部で参照されます。
  
  詳細については、[Polymer CLIを使用したエレメントプロジェクトの作成](https://www.polymer-project.org/2.0/docs/tools/create-element-polymer-cli)に関するガイドを参照してください。

* アプリケーションプロジェクト。アプリケーションプロジェクトでは、Polymerで構成されたアプリケーションを作成できます。このアプリケーションはWebサイトとして展開します。アプリケーションは自己完結型で、アプリケーション内のコンポーネントで構成されています。
  
  詳細については、[Polymer CLIを使用してアプリケーションプロジェクトを作成する](https://www.polymer-project.org/2.0/docs/tools/create-app-polymer-cli)ためのガイドを参照してください。

## Commands

コマンドとそれらの使用方法については、[Polymer CLI commands](https://www.polymer-project.org/2.0/docs/tools/polymer-cli-commands)を参照してください。

## Windows 10にPolymer CLIをインストールする前提条件 {#windows-10}

Windows 10システムでPolymer CLIの前提条件をインストールするには、複数の方法があります。ここでは、WindowsサブシステムのBashを使用します。

Bashの最新のインストール手順については、[WindowsのUbuntuに関するドキュメント](https://msdn.microsoft.com/en-us/commandline/wsl/about)を参照してください。

### Windows 10でBashを有効にする {#enable-bash}

1.  `Start > System > OS Build`の順に選択してOSの情報を確認する。
    
    Make sure you have an x64 installation of Windows 10 with OS build > 14393.
    
1.  `Settings > Update and Security > For developers`を開き、`Developer Mode`を選択します。

1.  Startメニューから、`Windows features on or off`を探して、`Windows Subsystem for Linux (beta)`を選択します。

1.  コンピューターを再起動します。

1.  `Administrator`でログインします。

1.  PowerShellプロンプトから、下記のコマンドを実行します：
    
        Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

1.  Bashプロンプトを開きます：
    
        bash

6.  プロンプトに従って新しいユーザーを作成します。

これでBashのインストールは完了です。Startメニューからbashと入力すると、新しいBashプロンプトを起動することができます。

### nvmでNodeをインストールする {#install-node}

最新の手順については、[nvmの公式ドキュメント](https://github.com/creationix/nvm)を参照してください。

1.  次のコマンドを入力して、インストールスクリプトを使用します：
    
        curl -o- https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash

2.  ターミナルを再起動してください。

3.  Nodeの最新バージョンをインストールします：

        nvm install node

### オプション：デフォルトブラウザ開く {#set-default-browser}

オプションで、`polymer serve --open`よりデフォルトブラウザで開くように設定します。Path変数を使用します。

    echo $'\n'export BROWSER=/mnt/c/Program\\\ Files\\\ \\\(x86\\\)/
    Google/Chrome/Application/chrome.exe >> ~/.bashrc
