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



