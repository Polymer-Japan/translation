> What are web components?  

### Web コンポーネントとは？  
 
> Web components are a set of web platform APIs that allow you to create new custom, reusable, encapsulated HTML tags to use in web pages and web apps. Custom components and widgets build on the Web Component standards, will work across modern browsers, and can be used with any JavaScript library or framework that works with HTML.

Webコンポーネントは、WebページやWebアプリケーションで使用するための、新しいエレメント、再利用、カプセル化されたHTMLタグを作成できるWebプラットフォームAPIのセットです。  
カスタムコンポーネントとウィジェットは、WebComponent標準をベースに構築され、最新のブラウザで動作し、HTMLで動作するJavaScriptライブラリやフレームワークで使用できます。

> Web components are based on existing web standards. Features to support web components are currently being added to the HTML and DOM specs, letting web developers easily extend HTML with new elements with encapsulated styling and custom behavior.  

Webコンポーネントは、Web標準に基づいています。
Webコンポーネントをサポートする機能は現在、HTMLおよびDOM仕様に追加されており、Web開発者がカプセル化されたスタイリングとカスタム動作を備えた新しい要素でHTMLを簡単に拡張できるようにします。  


> Specifications

### 仕様

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