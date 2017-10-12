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

## Shadow DOM ポリフィルについて

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



> Wrap all the objects!

#### すべてのオブジェクトをラップする

> The intent is to wrap all the DOM objects that interact with the DOM tree. 

DOMツリーと対話するすべてのDOMオブジェクトをラップすることです。

> For this polyfill to be completely transparent we need to wrap a lot of APIs.

このpolyfillを完全に透明にするには、多くのAPIをラップする必要があります。
 
> Any method, accessor or constructor that takes or returns a Node or an object that indirectly touches a node needs to be wrapped.

Nodeまたは、Nodeに間接的に接触するオブジェクトを受け取るか、返すメソッド、アクセサ、または、コンストラクタは、すべてラップする必要があります。
 
> As you can imagine there are a lot of these. 

このように、たくさんあります。

> At the moment we have done the most common ones but there are sure to be missing ones as soon as you try to use this with your code.

現時点では、最も一般的なコードを実行しましたが、コードでこれを使用しようとするとすぐに行方不明になることがあります。




> Wrap and Unwrap

#### Wrapと、Unwrap

> There are bound to be cases where we haven't done the wrapping for you. 

wrappingをしていない場合があります。

> In those cases you can use wrap to create a wrapper of a native object, or unwrap to get the underlying native object from a wrapper.

そのような場合は、ネイティブオブジェクトのwrapperを作成するためにwrapを使ったり、wrapperから基本的なネイティブオブジェクト取得するためにunwrapします

> These two functions are available on the ShadowDOMPolyfill object.

これらの2つの関数は、ShadowDOMPolyfillオブジェクトで使用できます。
 
> For example:

例

```javascript
wrap(document.body)
// or get body of the wrapped document
wrap(document).body

unwrap(div).firstChild instanceof HTMLElement
```

> If you plan to work with elements that need to be wrapped over and over, try passing a wrapped version of the element into an immediately-invoked function expression.

何度も繰り返す必要があるエレメントの場合は、エレメントのラップされたバージョンを、呼び出される関数に渡してみてください。

```javascript
(function(document) {
  // Now a library like jQuery can add
  // listeners to the wrapped document
  $(document).on('click', function(e) {
    console.log('Clicked on', e.target);
  });
})(wrap(document));
```


> Event Retargeting

#### イベントのリターゲット

> An important aspect of the shadow DOM is that events are retargeted to never expose the shadow DOM to the light DOM.

Shadow DOMの重要な側面は、Shadow DOMをLightDOMに公開しないようにイベントをリターゲットすることです。
 
> For example:

例

```javascript
var div = document.createElement('div');
div.innerHTML = 'Click me';
var shadow = div.createShadowRoot();
shadow.innerHTML = '<b><content></content></b>';
```

> If the user clicks on the div the real target of the click event is the `<b>` element. 

ユーザーが`div`をクリックすると、クリックイベントのターゲットは`<b>`エレメントになります。

> But that element is not visible in the light DOM so the target is therefore retargeted to the div element itself.

しかし、そのエレメントは`Light DOM`では表示されないので、ターゲットは`div`エレメント自体にリターゲットされます。
 
> However, if there is an event listener on the <content>, <b> or the shadow root, the target should be visible to the event listener.

ただし、`<content>`、`<b>`またはshadow rootにイベントリスナーがある場合、ターゲットはイベントリスナーに表示される必要があります。



> Similar issues occur with relatedTarget in mouseover and mouseoutevents.
  
`mouseover`や`mo​​useoutevents`の`relatedTarget`でも同様の問題が発生します。

> To support this kind of behavior the event dispatching in the browser has to be reimplemented by the polyfill.

この種類の動作をサポートするには、ブラウザでイベントをディスパッチするには、ポリフィルによって再実装する必要があります。



> Known limitations

#### 既知の制限事項

> CSS encapsulation is limited.
> Object.prototype.toString does not return the same string as for native objects.
> No live NodeLists. All node lists are snapshotted upon read.
> document, window, document.body, document.head and others are non configurable and cannot be overridden. 
We are trying to make these work as seamlessly as possible but there will doubtlessly be cases where there will be problems; 
for those cases you can use wrapand unwrap to get unblocked.
> Cross window/frame access is not implemented.
> CSS :host() rules can only have (at most) one level of nested parentheses in their argument selectors. For example, :host(.zot) and :host(.zot:not(.bar)) both work, but :host(.zot:not(.bar:nth-child(2))) does not.

- CSSのカプセル化には制限があります
- `Object.prototype.toString`は、ネイティブオブジェクトと同じ文字列を返すことが出来ません。
- ライブノードリストはありません。すべてのノードリストは、読み込み時にスナップショットされます。
- `document`、`window`、`document.body`、`document.head`などは設定できないため、上書きすることはできません。これらの作業を可能な限りシームレスに行うよう努めていますが、問題が生じるケースは間違いありません。そのような場合は、`wrap`と`unwrapを使用してブロックを解除することができます。
- クロス ウィンドウ/フレーム アクセスは実装されていません。
- CSS`:host()`ルールは引数セレクタにネストされたカッコを1レベルしか持てません。たとえば`:host(.zot)`と`:host(.zot:not(.bar))`はどちらも動作しますが、`:host(.zot:not(.bar:nth-​​child(2)))`は動作しません。



> Custom Elements polyfill

## カスタムエレメント ポリフィル

> The Custom Elements polyfill provides support for v0 of the Custom Elements spec. 
> A polyfill for v1 is in progress at https://github.com/webcomponents/custom-elements.

カスタムエレメント ポリフィルは、カスタムエレメント仕様のv0をサポートします。
v1のポリフィルは進行中です。[https://github.com/webcomponents/custom-elements](https://github.com/webcomponents/custom-elements)

> Custom elements polyfill handles element upgrades asynchronously. 

カスタムエレメント ポリフィルは、エレメントのアップグレードを非同期に処理します。

> The polyfill defers upgrading elements until DOMContentsLoaded time. 

ポリフィルは、`DOMContentsLoaded` 時間まで要素をアップグレードします。

> It does this as a performance optimization.

パフォーマンスの最適化としてこれを行います。
 
> Subsequent to the initial upgrade pass, Mutation Observers are used to discover new elements.
  
初期アップグレードに続いて、Mutation Observersを使用して新しいエレメントを発見します。

> To know when the polyfill has finished all of its start up tasks, listen to the WebComponentsReady event on document or window.

ポリフィルの起動タスクがすべてを完了したのを知るには、`document`または`window`の`WebComponentsReady`イベントを待ち受けます。
 
> For example:

例

```html
<script>
  // hide body to prevent FOUC
  document.body.style.opacity = 0;
  window.addEventListener('WebComponentsReady', function() {
    // show body now that everything is ready
    document.body.style.opacity = 1;
  });
</script>
```

> The Custom Elements specification is still under discussion.

カスタムエレメントの仕様はまだ議論中です。
 
> The polyfill implements certain features in advance of the specification.

ポリフィルは、仕様に先立って特定の機能を実装します。
 
> In particular, the lifecycle callback methods that get called if implemented on the element prototype:

特に、エレメントプロトタイプに実装されている場合に呼び出される、ライフサイクルコールバック・メソッドは実装されます

> createdCallback() is called when a custom element is created.
> attachedCallback() is called when a custom element is inserted into a DOM subtree.
> detachedCallback() is called when a custom element is removed from a DOM subtree.
> attributeChangedCallback(attributeName) is called when a custom element's attribute value has changed

- `createdCallback()`は、カスタムエレメントが作成されると呼び出されます。
- `attachmentCallback()`は、カスタムエレメントがDOMサブツリーに挿入されたときに呼び出されます。
- `detachedCallback()`は、カスタムエレメントがDOMサブツリーから削除されたときに呼び出されます。
- `attributeChangedCallback(attributeName)`は、カスタムエレメントの属性値が変更されたときに呼び出されます。


> createdCallback is invoked synchronously with element instantiation, the other callbacks are called asynchronously.

`createdCallback`はエレメントのインスタンス化と同期して呼び出され、他のコールバックは非同期に呼び出されます
 
> The asynchronous callbacks generally use the MutationObserver timing model,

非同期コールバックは、通常、`MutationObserver`タイミングモデルを使用します。
 
> which means they are called before layouts, paints, or other triggered events,

それは、レイアウト、ペイント、その他のトリガイベントの前に呼び出されることを意味します
 
> so the developer need not worry about flashing content or other bad things happening before the callback has a chance to react to changes.

ということから、開発者は、コールバックの変更前に起こるコンテンツのフラッシュやその他の悪い出来事について気にする必要はありません。


> HTML Imports Polyfill

## HTMLインポート ポリフィル

> In imported documents, href and src attributes in HTML, and urlproperties in CSS files, are relative to the location of the imported document, not the main document.

インポートされたドキュメントでは、HTMLの`href`と`src`属性、CSSファイルの`urlproperties`は、インポートされたドキュメントの相対位置になります。

> The HTML Imports polyfill begins processing link tags when the DOMContentLoaded event fires.

HTMLインポートポリフィルは、DOMContentLoadedイベントが発生したときにlinkタグの処理を開始します。
 
> To know when loading is complete, listen for the HTMLImportsLoaded event on document or window.

読み込みが完了したかは、documentまたはwindowのHTMLImportsLoadedイベントで検知できます。
 
> For example:

例:

```html
<script>
window.addEventListener('HTMLImportsLoaded', function(e) {
  // all imports loaded
});
</script>
```

> The polyfill loads linked stylesheets, external scripts, and nested HTML imports, but does not parse any data in the loaded resources.

ポリフィルでは、リンクされたスタイルシート、外部スクリプト、およびネストされたHTMLインポートはロードしますが、リソースのデータは解析しません。
 
> For parsing imports, combine HTML Imports with Custom Elements.

インポートを解析するには、HTMLインポートとカスタムエレメントを組み合わせます。
 
> As long as the HTML Imports is loaded first, the Custom Elements polyfill will detect it, and process all imports when HTMLImportsLoaded event fires.

HTMLインポートが最初にロードされると、カスタムエレメントポリフィルはそれを検出し、`HTMLImportsLoaded`イベントが発生した時にすべてのインポートを処理します。



> The WebComponentsReady event

## WebComponentsReady イベント

> Under native imports, <script> tags in the main document block the loading of imports. 

ネイティブのimportsでは、メインドキュメントの`<script>`タグがimportsの読み込みをブロックします。

> This is to ensure the imports have loaded and any registered elements in them have been upgraded.

これは、importsがロードされ、その中の登録されたエレメントがアップグレードされたことを保証するためです。


> This native behavior is difficult to polyfill so the HTML Imports polyfill doesn't try.

このネイティブの動作をポリフィルするのが難しいため、HTML imports ポリフィルでは対応していません。
 
> Instead the WebComponentsReady event is a stand in for this behavior:

その代わりに、`WebComponentsReady`イベントで、この動作をサポートしています

````html
<script>
  window.addEventListener('WebComponentsReady', function(e) {
    // imports are loaded and elements have been registered
  });
</script>
````

> In native HTML Imports, document.currentScript.ownerDocument references the import document itself. 

ネイティブのHTMLインポートでは、`document.currentScript.ownerDocument`はインポートドキュメント自体を参照します。

> In the polyfill, use document._currentScript.ownerDocument (note the underscore).

ポリフィルでは、`document._currentScript.ownerDocument`を使用します（アンダースコアに注意してください）。

