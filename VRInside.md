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
			* Oculus社はFacebook社に20億ドルで買収されている
			* https://www3.oculus.com/en-us/rift/
		* HTC Vive
			* HTC社とValve社が開発
			* ルームスケールVRをコンシューマ向けに展開した
			* ライセンス上ロケーションベースのVR（アミューズメントとか）と相性が良い
			* https://www.vive.com/jp/
		* PSVR
			* 我らがSONYが開発
			* PS4向けのVR端末
			* リリース4日で5万台弱を売った
			* （恐らく）世界で一番売れているハイエンドHMD
			* http://www.jp.playstation.com/psvr/
	* モバイルハイエンド
		* GearVR
			* Oculus社とSamsungの共同開発
			* MAUが100万人いる
			* GearVRとGearVR Readyのスマホとセットで動作可能
			* http://www.samsung.com/jp/product/gearvr/
		* Daydream View
			* Google社製のモバイルハイエンドの大本命
			* Daydream ViewとDaydream Readyのスマホとセットで動作可能
			* 日本での発売時期は未定
			* https://vr.google.com/daydream/headset/
	* モバイルローエンド
		* ハコスコ
			* 理化学研究所発のベンチャーが開発
			* ダンボール製、安い
			* 色々なスマホでVRコンテンツを楽しめる
			* https://hacosco.com/
		* MilboxTouch
			* ハコスコにタップ以外のインタラクティブ性を持たせている
			* 安い
			* タップやスワイプが出来るが、精度に難あり
			* http://milbox.tokyo/milboxtouch/
		* その他もろもろ
* VRコンテンツのプラットフォーム
	* Steam VR
		* PC向けのゲームプラットフォームであるSteamがVRにも対応
		* HTC Viveを作っているValve社が運営
		* 現在はWindowsのみ対応
		* 対応HMD
			* HTC Vive
			* Oclus Rift
	* Oculus Store（PC）
		* 対応HMD
			* Oculus Rift
		* Oculus Rift向けのプラットフォーム
		* 現在はWindowsのみ対応
	* Oculus Store（モバイル）
		* 対応HMD
			* Gear VR
		* GearVR Readyスマホ
			* Galaxy S7 edge
			* Galaxy S6 edge
			* Galaxy S6 
		* GearVR向けのプラットフォーム
		* PC向けのOculus Storeとは別にアプリ申請が必要
	* Daydream
		* 対応HMD
			* Daydream view
		* Daydream Readyスマホ
			* Pixel
			* Pixel XL
			* Moto Z
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
			* 言語
				* C#
				* JavaScript
			* 対応プラットフォーム
				* Oculus
				* HTC Vive
				* PSVR
				* Daydream
				* GearVR
				* モバイルローエンド
			* ライブラリ
				* Oculus SDK
				* Steam VR SDK
				* Google VR SDK
		* UE4
			* 言語
				* C++
			* 筆者はUE4を試していないのでざっくり
		* iOS(Xcode)
			* 言語
				* Objective-C
				* Swift
			* ライブラリ
				* Google VR SDK
		* Android(Android Studio)
			* 言語
				* Java
				* Kotlin
			* ライブラリ
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
