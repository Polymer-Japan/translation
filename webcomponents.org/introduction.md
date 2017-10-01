> What are web components?  

## Web コンポーネントとは？  
 
> Web components are a set of web platform APIs that allow you to create new custom, reusable, encapsulated HTML tags to use in web pages and web apps. Custom components and widgets build on the Web Component standards, will work across modern browsers, and can be used with any JavaScript library or framework that works with HTML.

Webコンポーネントは、WebページやWebアプリケーションで使用するための、新しいエレメント、再利用、カプセル化されたHTMLタグを作成できるWebプラットフォームAPIのセットです。  
カスタムコンポーネントとウィジェットは、WebComponent標準をベースに構築され、最新のブラウザで動作し、HTMLで動作するJavaScriptライブラリやフレームワークで使用できます。

> Web components are based on existing web standards. Features to support web components are currently being added to the HTML and DOM specs, letting web developers easily extend HTML with new elements with encapsulated styling and custom behavior.  

Webコンポーネントは、Web標準に基づいています。
Webコンポーネントをサポートする機能は現在、HTMLおよびDOM仕様に追加されており、Web開発者がカプセル化されたスタイリングとカスタム動作を備えた新しい要素でHTMLを簡単に拡張できるようにします。  


> Specifications

## 仕様

> Web components are based on four main specifications:

Webコンポーネントは、次の4つの仕様に基づいています。

#### Custom Elements  

> The Custom Elements specification lays the foundation for designing and using new types of DOM elements.

[Custom Elements](https://w3c.github.io/webcomponents/spec/custom/)仕様では、新しいDOMエレメント（HTML要素）の設計と使い方を定義しています  

#### Shadow DOM  

> The shadow DOM specification defines how to use encapsulated style and markup in web components.
  
[Shadow DOM](https://w3c.github.io/webcomponents/spec/shadow/)仕様では、Webコンポーネントでカプセル化されたスタイルとマークアップを使用する方法を定義しています。    

#### HTML imports

> The HTML imports specification defines the inclusion and reuse of HTML documents in other HTML documents.

[HTML imports](https://w3c.github.io/webcomponents/spec/imports/)仕様では、HTMLを他のHTMLに組み込むことと、再利用を定義しています。

#### HTML Template

> The HTML template element specification defines how to declare fragments of markup that go unused at page load, but can be instantiated later on at runtime.

[HTML Template](https://html.spec.whatwg.org/multipage/scripting.html#the-template-element/)仕様では、ページ読み込み時には使用されないが、後でインスタンス化できるマークアップのフラグメントを宣言する方法を定義しています。

> How do I use a web component?
## web componentの使い方

> The components on this site provide new HTML elements that you can use in your web pages and web applications.

このサイトのコンポーネントは、zWebページや、Webアプリケーションで使用できる 新しいHTMLエレメントを提供します。

> Using a custom element is as simple as importing it, and using the new tags in an HTML document. For example, to use the Emoji Rain element:

Custom Elementsを使用するのは、HTMLエレメントをインポートし、HTMLで新しいタグを使用するだけです。  
たとえば、[Emoji Rain エレメント](https://www.webcomponents.org/element/notwaldorf/emoji-rain)を使用するには、次のようにします。

```html
<link rel="import" href="../emoji-rain/emoji-rain.html">
...
<emoji-rain active></emoji-rain>
```

> There are a number of ways to install custom elements.
 
Custom Elementsをインストールするにはいくつかの方法があります。

> When you find an element you want to use, look at its README for the commands to install it.

使いたいHTMLエレメントを見つけたら、READMEからインストールするためのコマンドを探して下さい。
 
> Most elements today can be installed with Bower. 

ほとんどのHTMLエレメントはBowerからインストールが行えます。

> Bower also handles installing the components' dependencies. 

Bowerは、コンポーネントの依存関係のインストールも行います。

> For more information on Bower, see Bower.io.

その他の情報については、Bowerの[公式サイト](https://bower.io/)を見て下さい。



> For example, the Emoji Rain README describes the install process with Bower:

たとえば、[Emoji Rain のREADME](https://www.webcomponents.org/element/notwaldorf/emoji-rain)では、Bowerを使ったインストール方法を以下のように説明されています。

```
mkdir emoji-rain-demo && cd emoji-rain-demo
bower install emoji-rain
```

> How do I define a new HTML element?
## 新しいHTMLエレメントを定義するにはどうすればよいですか？

> This section describes the syntax for the new cross-browser version (v1) of the Web Components specification.

このセクションでは、Webコンポーネントの構文（v1）について説明します。

> Use JavaScript to define a new HTML element and its tag with the customElements global. 

まずは、JavaScriptを使用して、新しいHTMLエレメントとそのタグを、Custom Elementsとして定義します。

> Call customElements.define() with the tag name you want to create and a JavaScript class that extends the base HTMLElement.

`customElements.define()`に、新しく作成するタグの名前と、HTMLElementを拡張した、JavaScriptクラスを指定して呼び出します。

> For example, to define a mobile drawer panel, <app-drawer>:

たとえば、mobile drawer panel（`<app-drawer>`）を定義するには以下のようにします。

```html
class AppDrawer extends HTMLElement {...}
window.customElements.define('app-drawer', AppDrawer);
```

> v0 of the Custom Elements specification used document.registerElement() for this purpose:

Custom Elementsのv0では、`document.registerElement()`を使用しました。

```html
var XFoo = document.registerElement('x-foo');
document.body.appendChild(new XFoo());
```

> See this article on the v0 Custom Elements specification for more information. To use the new tag:

Custom Elements(v0)の詳細については、[この記事](https://www.html5rocks.com/en/tutorials/webcomponents/customelements/)を参照してください。  
定義したタグを使用するには以下のようにします。

```html
<app-drawer></app-drawer>
```

> Using a custom element is no different to using a <div> or any other element. 

Custom Elementsの使い方は、`<div>`など、これまでのHTMLエレメントを使う時と変わりありません。

> Instances can be declared on the page, created dynamically in JavaScript, event listeners can be attached, etc.

その他にも、インスタンスをページ上で宣言したり、JavaScriptで動的に作成したり、イベントリスナーをアタッチすることなどもできます。

```html
<script>

    // Create with javascript
    var newDrawer = document.createElement('app-drawer');
    
    // Add it to the page
    document.body.appendChild(newDrawer);
    
    // Attach event listeners
    document.querySelector('app-drawer').addEventListener('open', function() {...});
</script>
```