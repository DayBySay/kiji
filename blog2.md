前編の続きです。

# 目次

[:contents]

# A-Frame + A-Frame Boilerplateを使ってWebVRアプリを開発する
さっそくですが、A-Frameを利用してWebVRアプリを作ってみたいと思います。

今回は`git`と`npm`を利用するので、これらのコマンドを使えるようにしておいて下さい。

## A-Frame Boilerplateについて
`A-Frame Boilerplate`は、次の3つの機能を備えています。

* 最新のA-FrameにリンクされたHTMLファイル
* ローカルの開発サーバ
* [Github Pages](https://pages.github.com/)に簡単にデプロイする機能

要はA-Frameを利用したアプリの開発環境を簡単に整えられる仕組みですね。

## ローカル開発環境の準備
まずは`A-Frame Boilerplate`をローカルにクローンします。

```
git clone https://github.com/aframevr/aframe-boilerplate.git
cd aframe-boilerplate && rm -rf .git && npm install
```

この状態で`npm start`を実行すると、ブラウザが開きA-Frameアプリケーションが表示されます。

[f:id:DayBySay:20161217232848p:plain]

これでローカルの開発環境は準備OKです。簡単！

次に、スマホで動作確認できるようにアプリケーションをWeb上に公開しましょう。

## スマートフォンで動作確認するための環境準備
公開方法にこだわりがない & GitHubアカウントをお持ちの方は`GitHub Pages`を利用しましょう。

先述の通り、`A-Frame Boilerplate`が`GitHub Pages`へのデプロイをサポートしているので、簡単に公開できます。

まずはGitHubに公開リポジトリを作ります。

[f:id:DayBySay:20161217232938p:plain]

今回は `https://github.com/DayBySay/my-aframe-application` として作成しました。

次に、先程の`aframe-boilerplate`ディレクトリのリモートリポジトリとして、今作成したリポジトリを登録します。

```
git init
git remote add origin git@github.com:<UserName>/<RepositoryName>.git # <UserName> と <RepositoryName> は書き換えて下さい
git add .
npm run deploy
```

これでアプリケーション公開の準備が整いました。

スマートフォンで `https://<UserName>.github.io/<RepositoryName/` を開き、右下のカードボードマークをタップすると下記のような画面が現れると思います。

[f:id:DayBySay:20161217173409j:plain]

すでに立体視になっていますね！しかもこの時点でヘッドトラッキングにも対応しています！

これで開発 -> スマホで動作確認のサイクルを回せるようになりました。

## A-Frameで文字を表示する
せっかくなので少し実装をしてみましょう。

まずは `Hello World` という文字を表示するところまでやってみたいと思います。

A-Frameでテキスト表示する方法はいくつかありますが、[公式に推奨されている](https://aframe.io/docs/0.4.0/introduction/faq.html#how-do-i-display-text-in-a-frame)のは`Bitmap Font Text Component`を利用する方法です。

ここで行うのは

* Bitmap Font Text Componentのscriptをを読み込む
* Bitmap Font Text Componentのコンポーネントを追加する

です。

ディレクトリ直下の`index.html`を下記のように変更して下さい。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Hello, World! - A-Frame</title>
    <meta name="description" content="Hello, World! - A-Frame">
    <script src="https://aframe.io/releases/0.4.0/aframe.min.js"></script>
    <script src="https://rawgit.com/bryik/aframe-bmfont-text-component/master/dist/aframe-bmfont-text-component.min.js"></script>
  </head>
  <body>
    <a-scene>
      <a-camera>
        <a-entity id="text" position="-0.6 0.1 -1"
          bmfont-text="color: black; text: Hello World;">
        </a-entity>
      </a-camera>

      <a-box position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9"></a-box>
      <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
      <a-cylinder position="1 0.75 -3" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>
      <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>

      <a-sky color="#ECECEC"></a-sky>
    </a-scene>
  </body>
</html>
```

`<a-camera>`の下に`Bitmap Font Text Component`を追加したので、常に自分の目の前にテキストが表示されるようになっています。

これをコミットし、また`npm run deploy`でデプロイしましょう。

スマートフォンで先程のURLを更新すると、下記の画像のような表示になっていると思います。

[f:id:DayBySay:20161218015045j:plain]

文字が表示できました！

## 動的に文字を変えてみる
文字の表示は出来ましたが、これだとインタラクション性が皆無なので面白くないです。

そこで、先程追加したテキストエリアに、自分が見ているオブジェクトの名前を表示できるような機能を追加しましょう！

ここで行うのは

* クリックが出来るようにカーソルを追加し、特定の時間見つめるとクリックが発火されるような実装(いわゆるフューズ)にする
* クリックの発生時にオブジェクトのidを取得して、テキストエリアにidを代入するscriptを実装する
* オブジェクトに対して上記リスナーを追加する(ついでに表示名用のidも追加)

です

`index.html`を下記のように変更して下さい。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Hello, World! - A-Frame</title>
    <meta name="description" content="Hello, World! - A-Frame">
    <script src="https://aframe.io/releases/0.4.0/aframe.min.js"></script>
    <script src="https://rawgit.com/bryik/aframe-bmfont-text-component/master/dist/aframe-bmfont-text-component.min.js"></script>
    <script>
      AFRAME.registerComponent('cursor-listener', {
        init: function () {
          this.el.addEventListener("click", function (evt) {
            document.getElementById("text").setAttribute("bmfont-text", "text", this.getAttribute("id"));
          });
        }
      });
    </script>
  </head>
  <body>
    <a-scene>
      <a-camera>
        <a-cursor
          fuse="true"
          fuse-timeout="500"
          position="0 0 -1"
          material="color: blue; shader: flat">
        </a-entity>
        <a-entity id="text" position="-0.6 0.1 -1"
          bmfont-text="color: black;">
        </a-entity>
      </a-camera>

      <a-box id="box" cursor-listener position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9"></a-box>
      <a-sphere id="sphere" cursor-listener position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
      <a-cylinder id="cylinder" cursor-listener  position="1 0.75 -3" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>
      <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>

      <a-sky color="#ECECEC"></a-sky>
    </a-scene>
  </body>
</html>

```

まずは`<a-camera>`の下に`<a-cursor>`を追加し、見ている場所をクリック出来るようにしています。

次に`AFRAME.registerComponent`で`cursor-listener`コンポーネントを定義し、`<a-box>`などのオブジェクトに追加しました。

これによって、オブジェクトがクリックイベントを受け取った時に、`AFRAME.registerComponent`で定義されたスクリプトを実行するようになります。

`<a-cursor>`は`fuse`がtrueの場合、`fuse-timeout`で設定されている値で自動的に`click`イベントを対象オブジェクトに送信するので、今回は0.5秒間見つめることで、クリックする事が出来ます。

イベントの実装はシンプルで、`id`ベースで`bmfont-text`のコンポーネントを取得し、`text`属性に自身の`id`を代入するだけです。

これをコミットし、また`npm run deploy`しましょう。

下記の画像のように、見つめたものの名前が表示されていれば成功です！

![gif](https://media.giphy.com/media/l4JyVCLyfCcSy8o6c/giphy.gif)

ちなみに日本語を表示する場合は少し頑張る必要があるのですが、それについて[弊社ブログの記事](http://vr-lab.voyagegroup.com/entry/2016/11/16/122115)にまとめているので、ぜひご参照下さい！

# 後編のまとめ
* WebVRアプリ開発はA-FrameとA-Frame Boilerplateで簡単に初められる！
* A-Frameでテキスト表示するには`Bitmap Font Text Component`を利用する

以上、VR開発の概要からWebVRアプリの開発環境構築まで一通り説明させていただきました。

スマートフォンで我々の生活を大きく変わったように、VRも我々の生活を良い方向に進めてくれると信じています。そんな未来を早く実現するためにも、みんなで素晴らしいVRアプリケーションをガンガン作っていきましょう！

ちなみにVOYAGE GROUPではVRアプリケーションを開発したいエンジニアやクリエイターの方を募集しておりますので、[Twitter](https://twitter.com/daybysay)などでお気軽にお声がけ下さい！

それでは、よいVRアプリケーション開発ライフを！
