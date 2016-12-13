# VRInside寄稿
## テーマ
* 最初に開発を開始する中での注意点からどういう場合にはどのような環境がおすすめか？マルチデバイス対応をするには、こんな環境がおすすめ？
* 開発者向けなので、既に開発が可能なHMDやプラットフォームについて言及する
* 開発環境の特性、使用言語、利用可能ライブラリ・開発支援ツールなどを厚めに

## コンテンツ
* 世の中のHMDについて
	* ハイエンド
		* Oculus Rift
			* 2012に登場 Kicksterter
				* https://www.kickstarter.com/projects/1523379957/oculus-rift-step-into-the-game
			* VRブームの火付け役
			* 最近ハンドルコントローラの Oculus Touchをリリース
			* https://www3.oculus.com/en-us/rift/
		* HTC Vive
			*
			* https://www.vive.com/jp/
		* PSVR
			* http://www.jp.playstation.com/psvr/
	* モバイルハイエンド
		* GearVR
			* http://www.samsung.com/jp/product/gearvr/
		* Daydream
			* https://vr.google.com/daydream/headset/
	* モバイルローエンド
		* ハコスコ
			* https://hacosco.com/
		* MilboxTouch
			* http://milbox.tokyo/milboxtouch/
		* その他もろもろ
* VRのプラットフォーム
	* Steam
		* HTC Vive
		* Oclus Rift
	* Oculus Store
		* Oculus Rift
		* Gear VR
	* Daydream
		* Daydream
			* https://vr.google.com/daydream/
	* WebVR
		* HTC Vive
		* Oculus Rift
		* モバイルローエンド全般
	* AppStore, GooglePlay
		* モバイルローエンド全般
* VRのコンテンツ開発
	* ネイティブVRアプリケーション
	* WebVRアプリケーション
* 開発環境
	* ネイティブVR
		* Unity
			* C#
			* (Unity Script)
			* Oculus SDK
			* Steam VR SDK
		* UE4
			* C++
			* 筆者はUE4を試していないので割愛
		* iOS(Xcode)
			* Google VR SDK
		* Android(Android Studio)
			* Google VR SDK
	* WebVR
		* HTML, JS
			* Three.js
				* https://threejs.org/
			* A-Frame
				* https://aframe.io/
			* Solufa
				* http://solufa.io/
* 開発時の注意点
	* VR酔いを防ぐ
		* FPSを高く保つ
		* ヘッドトラッキングを止めない
		* 等速移動を心がける
		* 視野内で更新される情報を減らす
	* VRに即したインターフェイスを使う
		* ハンドルコントローラ
		* レティクル
		* ヒューズボタン
	* 開発と動作確認のサイクル
		* HMDをつけたり外したりするのが大変
			* 後肩がこる
		* EnvelopVRみたいな、ずっとHMDをつけていられる環境を用意したい
			* あるいは開発者と動作確認者を分ける
