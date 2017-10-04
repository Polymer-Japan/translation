# Polyfills

> Some browsers are still in the process of updating to support the standards for Web Components.

一部のブラウザでは、Web Componentsの実装が終えておらず、更新途中となっております。
 
> In the mean time, polyfills simulate the missing browser capabilities as closely as possible. 

その間、ポリフィルが実装前の機能を、できるだけ実装に近い形に再現してくれます。



> You can feature-detect for the necessary browser features before loading the polyfills.

ポリフィルをロードする前に、必要なブラウザ機能を検出することができます。
 
> This means that as more and more browsers implement the Web Components standards, the payload to run your apps and elements will decrease.

つまり、Web Componentsの標準化を実装するブラウザが増えれば、アプリケーションやエレメントを実行するペイロードが減少します。

> The polyfills are available on GitHub: [https://github.com/WebComponents/webcomponentsjs](https://github.com/WebComponents/webcomponentsjs)

ポリフィルはGitHubにて取得可能です。

> To install the polyfills, run this command:

ポリフィルをインストールするには、次のコマンドを実行します。

```
bower install --save webcomponents/webcomponentsjs
```

> To feature detect:

検出機能を使用するには、以下のようにします。

```javascript
(function() {
  if ('registerElement' in document
      && 'import' in document.createElement('link')
      && 'content' in document.createElement('template')) {
    // platform is good!
  } else {
    // polyfill the platform!
    var e = document.createElement('script');
    e.src = '/bower_components/webcomponentsjs/webcomponents-lite.min.js';
    document.body.appendChild(e);
  }
})();
```

> Shadow DOM polyfill

Shadow DOM ポリフィルについて

> The shadow DOM polyfill provides shadow DOM v0 functionality in browsers that don't support it natively.

Shadow DOM ポリフィルは、Shadow DOMに対応していないブラウザにShadow DOM(v0)の機能を提供します。
 
> See the Compatibility table for more information.

詳細は互換性表を参照してください。



> The shadow DOM polyfill, though very powerful, is also fairly intrusive and can add significant performance overhead.

Shadow DOM ポリフィルは非常に強力ですが、パフォーマンスオーバーヘッドを招くおそれがあります。

> For this reason, many Web Components-based libraries like Polymer work around having to use this polyfill, and provide a lighter-weight alternative.

このため、Polymerなど、Webコンポーネントベースのライブラリでは、このポリフィルは使わずに軽量の代替品を使用します
 
> These libraries don’t require loading the full Web Components polyfill, but instead use a “lite” version of the polyfill with shadow DOM removed:

これらのライブラリは、完全なWeb Components ポリフィルは使わずに、Shadow DOMを削除した「ライト」バージョンのポリフィルを使用します。

```
webcomponents/webcomponents-lite.min.js
```