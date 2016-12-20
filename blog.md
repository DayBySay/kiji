こんにちは。株式会社VOYAGE GROUP VR LAB室の[@daybysay](https://twitter.com/daybysay) と申します。普段はインターネット広告のSDKエンジニアをしております。

今年の10月にVR LAB室を社内で立ち上げ、そちらでちょろちょろとVRアプリの開発をやっています。

今回は、これからVRコンテンツを開発する人向けに前編でVRの開発環境周りをまとめ、後編で実際にVRコンテンツの開発をやってみよう！という内容で書いてみました。

今後、素敵なVRコンテンツ開発ライフを過ごすための参考にして頂ければなーと思います。

# 目次

[:contents]

# VRアプリケーション開発が出来るHMD(Head Mounted Display)について

開発を始める上で、そもそも**どんなコンテンツが作れるのか？**を知る必要があります。

VRにおいては、360°見渡せる体験が出来るコンテンツ開発が可能なのですが、利用するHMDによって操作方法が違ったりします。

まずはどんなHMDが存在していて、それぞれどういう特徴があるのかをおさらいしましょう。

[f:id:DayBySay:20161217233003p:plain]

2016年末現在、VRアプリケーション開発が出来るHMDは下記2つに大別できます。

* ハイエンドHMD
* モバイルHMD

## ハイエンドHMD
[f:id:DayBySay:20161217232944j:plain]

ハイエンドHMDは、いわゆる**ゲーミングPC**などの据え置き型の端末とセットで使うHMDで、次のような特徴があります。

**良い点**

* ディスプレイのリフレッシュレートが高いため、高FPSで酔いづらいアプリケーションの開発が可能
* ルームスケールに対応しているため、コンテンツ内を歩き回る体験を作り出せる
* 多くの場合ハンドコントローラに対応しているため、VR空間内にユーザの手を再現でき、インタラクションの幅が広い

**悪い点**

* ゲーミングPCとHMDが必要なため、初期のコストが高い(合わせて20万~)
* ルームスケールのコンテンツを体験する広いスペースを用意するのが大変

3Dお絵かきアプリである[TiltBrush](https://www.tiltbrush.com/)や、VR空間で他のユーザと遊べる[Toybox](https://www.oculus.com/experiences/rift/1083042371786607/)など、全身を使う動きのあるコンテンツとの相性が良いです。

**TiltBrush**
<iframe width="560" height="315" src="https://www.youtube.com/embed/TckqNdrdbgk" frameborder="0" allowfullscreen></iframe>

## モバイルHMD
[f:id:DayBySay:20161217233011j:plain]

モバイルHMDは、スマートフォン + HMDで利用できる端末で、ハイエンドのHMDに比べるとインタラクションの種類が限定されてしまったり、扱えるポリゴン数が少ないなど、制約が多いです。

しかし、スマートフォンユーザなら安価なHMDを買うだけでVRコンテンツを体験できるので、体験までのコストは低いです。((Galaxy, Pixelユーザ以外はローエンドに限る))

また、モバイルHMDの中でもハイエンドとローエンドで分かれており、モバイルハイエンドのHMDは没入感が高いコンテンツが結構あります。

**良い点**

* 安いHMD + お手持ちのスマホでコンテンツが体験できるので、コンテンツ体験までのハードルが低い(**1,000円~**)
* HMD + スマホで動作するのでハイエンドHMDと違って場所を選ばない
* (モバイルハイエンド) ハイエンドHMDには劣るものの、ユーザの色々な入力を受けるインターフェイスが備わっている
* (モバイルローエンド) 既存のストアを利用してアプリを配布できる為、潜在的なユーザが多い((例えばGoogleCardboardのユーザは今年の1月時点で[世界で500万以上](https://blog.google/products/google-vr/unfolding-virtual-journey-cardboard/)。ちなみにGearVRのMAUは100万人以上と[公式に発表されている](http://fortune.com/2016/05/11/oculus-samsung-gear-1-million-users/)))

**悪い点**

* 現状のモバイルHMDだと**ポジショントラッキングができない**ので、ユーザの自身の現実世界での移動をコンテンツに反映するのが難しい((加速度や角速度センサーの値を使えば多少は可能である))
* (モバイルローエンド) 多くの場合ハンドコントローラがないので、コンテンツ内のインタフェイスが視線ベースになることが多く、目と首が疲れやすい
* (モバイルローエンド) スマホのスペックによって扱えるポリゴン数などにかなり差があるので調整が大変

モバイルHMDは場所に関係なく使えるので、例えばNetflixやYoutubeのような動画を見るコンテンツや、リラクゼーション系など、頭だけで使えて動きが少ないコンテンツと相性が良いです。

**Youtube VR**
<iframe width="560" height="315" src="https://www.youtube.com/embed/ROzDHcayl-k" frameborder="0" allowfullscreen></iframe>

これら特性をしっかり把握した上で、どのHMD向けにコンテンツを提供していくか検討をするのが重要です。

# ネイティブかWebか
次にVRアプリケーションの種類についてです。

スマートフォンで利用できるアプリケーションと同様に、VRにおいても**ネイティブ**と**Web**があります。

これらもそれぞれ特徴があるのでおさらいしましょう。

## ネイティブ
ネイティブVRアプリは下記のような特徴を持っています

* WindowsやMacOS、GearVRやDaydreamなどのアプリストア経由でインストールして利用できるアプリケーション
* Unity、 UE4などのゲームエンジンがVR対応をしており、ゲーム開発をされていた人が参入しやすい
* Oculus RiftやHTC ViveなどのベンダからHMD用の公式SDKが提供されている
* WebVRに比べてリッチで作り込まれた表現がし易いのと、（多くの場合）Wi-Fiか有線が前提なのでネットワークの制約を気にしなくても良い

いま世の中に存在するVRコンテンツの殆どはネイティブで作られています。

元々UnityやUE4などでゲーム開発をしていた人はすぐに初められるので、ゲームエンジニアの方にお勧めです。

### ネイティブの開発環境
[f:id:DayBySay:20161217233044p:plain]

ネイティブのVRコンテンツ開発は、多くの場合下記2つのゲームエンジンで行われています。

* [UNREAL ENGINE4(UE4)](https://www.unrealengine.com/ja/what-is-unreal-engine-4)
* [Unity](https://unity3d.com/jp/)

それぞれ特性がありますが、**モバイルに強く情報量が多い**Unityと、**リアルなグラフィックに強く、ブループリントという使いやすいビジュアルスクリプト言語を擁する**UE4というのがざっくりした特徴です。

ちなみに私がネイティブを開発する際はは基本的にUnityを使っており、UE4をほぼ触っていないため、ここでは紹介程度とさせていただきます。

### UnityによるネイティブVRアプリ開発
UnityにおけるVRアプリケーション開発は、基本的にベンダの提供しているSDKを利用します。

例えばHTC Vive向けには[SteamVR SDK](https://www.assetstore.unity3d.com/jp/#!/content/32647)がAssetStore((Unityの開発に使えるアセットが売買出来るプラットフォーム))上に存在しており、そちらを利用して行います。

HTC Vive向けの開発については[弊社ブログの過去記事](http://vr-lab.voyagegroup.com/entry/2016/09/28/120925)で公開しているので、そちらをご参照下さい。

また、モバイルのGoogleCardboardやDaydream向けの開発では[Google VR SDK](https://developers.google.com/vr/unity/)を利用します。

こちらも[弊社ブログの過去記事](http://vr-lab.voyagegroup.com/entry/2016/11/07/235026)で公開しているので、そちらをご参照下さい。

## WebVR
WebVRアプリは下記のような特徴を持っています

* Web上にホスティングされ、ブラウザでURLにアクセスするだけで簡単に体験できるアプリケーション
* 基本的には[WebVR API](https://github.com/w3c/webvr)を利用して開発を行う
* WebVR APIはHMD本体、HMD用カメラ(ポジショントラッキング)とブラウザの間をつなぐAPIで、Web GL、Web Audio、GamePad APIと組み合わせてアプリケーションを開発する

WebVR APIを正式実装しているブラウザはまだ存在せず、[W3CにWebVR APIのドラフトが出ている段階](https://w3c.github.io/webvr/)です。

現在は多くのコンテンツがネイティブアプリケーションで作られていますが、開発環境やブラウザのWebVR API対応によって、今後はWebアプリケーションも増えてくると予想されます。

ちなみにブラウザのWebVR API対応状況に関しては [Is WebVR Ready?](https://iswebvrready.org/) で確認が可能です。

### WebVRの開発環境
[f:id:DayBySay:20161217233050p:plain]

当然ですが、WebVRはHTML + CSS + JSでの開発が可能です。

また、WebVR開発支援のライブラリが存在しており、それらを活用すると簡単にWebVRアプリ開発が可能です。

現在WebVRで利用可能なライブラリは下記です。

* [WebVR Boilerplate](https://github.com/borismus/webvr-boilerplate)
* [React VR](https://github.com/facebookincubator/react-vr)
* [A-Frame](https://github.com/aframevr/aframe/)

これらはJSの3Dライブラリである[Three.js](https://github.com/mrdoob/three.js/)をベースに実装されています。

ライブラリ内にWebVR APIのラッパーが存在するので、Oculus RiftやHTC ViveなどのハイエンドHMD、ハンドコントローラなどの情報も簡単に扱うことが可能です。

例えば、A-Frameで作られている[A-Painter](https://aframe.io/a-painter/)というアプリは、HTC ViveでリリースされているTiltBrushのように、HTC Viveのコントローラを使ったお絵かきアプリをWebVRで実現しています！

**A-Painter**

![A-paniter](https://blog.mozvr.com/content/images/2016/09/apainter_painting.gif)

### React VR
React VRは先日の[Oculus Connectで発表された](https://techcrunch.com/2016/10/06/oculus-webvr/)Facebook謹製のライブラリで、現時点ではまだプレリリース状態です。

[React Native](https://facebook.github.io/react-native/)をベースに作られており、JSの独自拡張構文である[JSX](http://facebook.github.io/jsx/)を利用した開発が可能になっています。

React VRについての詳細は[公式のブログ](https://developer.oculus.com/blog/introducing-the-react-vr-pre-release/)に書かれております。

React VR自体は[こちら](https://s3.amazonaws.com/static.oculus.com/reactvr/React_VR_Prerelease.zip)から直接ダウンロードして利用することが出来ます。

少しだけ触りましたが、JSXを初めて触ったのでちょっと戸惑いました。また、初回のアクセス時にreact native packerが行うアプリのビルドに結構時間がかかるので、お手軽感に欠けるかなーと思いました。

このあたりはReactやReact VRの勉強をもう少ししてから、また記事にしたいと思います。

### A-Frame
A-FrameはWeb開発を支援するため、Mozilla VRチームが中心となって開発しているOSSのライブラリで、HTMLでVRアプリケーションを作成するためのオープンソースのWebVRフレームワークです。

独自のHTML拡張構文が用意されているのと、[A-Frame Inspector](https://github.com/aframevr/aframe-inspector)というビジュアルエディタが用意されているのが特徴です。

[先日リリースされたA-Frame v0.4.0](https://aframe.io/blog/aframe-v0.4.0/)では、新たに[A-Frame Registory](https://aframe.io/aframe-registry/)が公開されました。

これはUnityで言うところのAssetStoreの様なものであり、Registoryに登録されているコンポーネントを上記のInspectorから直接利用出来るという便利な機能を備えています。

WebVRアプリ開発を始めるに当たって、一番お勧めしたいのは**A-Frame + [A-Frame-Boilerplate](https://github.com/aframevr/aframe-boilerplate)**です。

# 前編まとめ
ここまでのまとめです。

* HMDにはハイエンドとローエンドがあり、ものによってコントローラが違う
* アプリのタイプにはネイティブとWebがあり、それぞれに特徴がある

後編では、A-Frameを利用して簡単なWebVRアプリケーションを作ってみたいと思います。

お手元にスマートフォンがある方は是非トライしてみて下さい。

後編へ続く
