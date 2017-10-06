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

### Shadow DOM ポリフィルについて

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

> Wrappers

#### Wrappers

> The polyfill is implemented using wrappers.

ポリフィルはwrappersを使用して実行されています。
 
> A wrapper wraps the native DOM node in a wrapper node. 

wrapperはネイティブDOMノードをラッパー・ノードでラップします。

> The wrapper node looks and behaves identically to the native node (minus bugs and known limitations).

ラッパー・ノードは、ネイティブ・ノードのように振る舞います（バグと既知の制限はありません）。
 
> For example:

例：

```javascript
var div = document.createElement('div');
div.innerHTML = '<b>Hello world</b>';
assert(div.firstChild instanceof HTMLElement);
```

> But div is actually a wrapper of the element that the browser normally gives you.

実際は`div`は通常のエレメントのラッパーになります。
 
> This wrapper just happens to have the same interface as the browser provided element.

このラッパーは、ブラウザーで提供されるエレメントと同じインターフェースを持ちます。




> It has an innerHTML setter that works just like the native innerHTML but instead of working on the composed tree it works on the local DOM. 

これには`innerHTML`セッターがあります。これはネイティブ`innerHTML`のように機能しますが、作成されたツリーで動作するのではなく、ローカルDOM上で動作します。

> When you change the logical DOM tree like this it might cause the composed tree to need to be re-rendered. 

このように論理DOMツリーを変更すると、作成されたツリーを再レンダリングする必要が生じる可能性があります。

> This does not happen immediately, but it is scheduled to happen later as needed.

これはすぐには起こらないが、必要に応じて後で起こる予定である。




> The wrapper node also has a firstChild getter which once again works on the logical DOM. 

ラッパー・ノードには`firstChild`ゲッターもあり、これは論理DOMで再び動作します。

> instanceof still works because we have replaced the global HTMLElementconstructor with our custom one.

`instanceof`は、グローバルなHTMLElementコンストラクタをカスタムコンストラクタに置き換えたので、動作します。



> More Logical DOM

#### 論理DOMについて

> The `wrappers.Node` object keeps track of the logical (light as well as shadow, but not composed) DOM. 

`wrappers.Node`オブジェクトは、論理DOMを追跡します（ライトとシャドウですが、合成されていない）

> Internally it has has the 5 fundamental Node pointers: parentNode, firstChild, lastChild, nextSibling and previousSibling.

内部的には、`parentNode`、`firstChild`、`lastChild`、`nextSibling`、`previousSibling`、の5つのNode pointerがあります。
 
> When the DOM tree is manipulated, these pointers are updated to always represent the logical tree. 

DOMツリーが操作されると、これらのポインタは常に論理ツリーを表すために更新されます。

> When the shadow DOM renderer needs to render the visual tree, these internal pointers are updated as needed.

Shadow DOMレンダラがビジュアルツリーをレンダリングする必要がある場合、これらの内部ポインタは必要に応じて更新されます。

