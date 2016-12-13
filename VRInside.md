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
		* 対応HMD
			* HTC Vive
			* Oculus Rift
			* モバイルローエンド全般
		* WebVR APIによってハイエンドHMDのAPIが利用可能
		* WebVR APIはDeveloper版のブラウザでのみ利用可能
			* Chromium
				* https://webvr.info/get-chrome/
			* Firefox ナイトリービルド
				* https://www.mozilla.org/ja/firefox/channel/desktop/#nightly
	* AppStore, GooglePlay
		* モバイルローエンド全般
		* 通常のAppStoreやGooglePlayと同様のフローで申請可能
* VRのコンテンツ開発
	* ネイティブVRアプリケーション
		* 特徴
			* WindowsやMacOS、GearVRやDaydreamなどのプラットフォーム経由でアプリケーションをインストールして利用できるネイティブアプリケーション
			* Unity, UE4など、VRコンテンツ開発をサポートする強力なゲームエンジンが存在する
			* Oculus RiftやHTC Viveなどベンダの公式からSDKが提供されている事が多い
			* OSネイティブのAPIを叩けるので出来ることの幅が広い
			* WebVRに比べてリッチで作り込まれた表現がし易いのと、（多くの場合）Wi-Fiか有線が前提なので扱うファイルサイズの制約が少ない
	* WebVRアプリケーション
		* 特徴
			* Web上にホスティングされ、インストール不要で簡単に体験できるアプリケーション
			* ブラウザベースなのでURLのみでアクセス可能
			* A-Frameなど、ブラウザ上でVRを実現するためのライブラリが存在する
			* Web VR APIがまだ策定中なので開発版のブラウザでないと一部のAPIの利用に制約がある
				* Web VR APIはHMD、HMD用カメラ(ポジショントラッキング)とブラウザの間をつなぐもの
			* 基本的には Web VR, Web GL, Web Audio, GamePad APIの組み合わせでアプリケーションを開発する
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
* おすすめの開発環境
	* 簡単に開発を初めたい人向け
		* A-Frameを使ったWebVRアプリケーション開発
			* ハコスコ(1,000円くらい)があれば体験可能
			* MozillaのVRチームが開発しているOSS
			* Web技術者が簡単に参入可能
			* A-Frame Inspectorなどの便利ツールがある https://github.com/aframevr/aframe-inspector
			* 2,000人が参加している slackがある https://aframe.io/community/
			* VGのVR Lab室で(ry
	* リッチで作り込まれたコンテンツ開発がしたい人向け
		* Unityを使ったネイティブアプリケーション開発
			* 特にPC向けだと利用できるポリゴン数が大きい
			* Unityはシェアが大きいので情報量が多い
			* 困ったときに質問できる場所がある
				* Unity ユーザ助け合い所 https://www.facebook.com/groups/unityuserj/
				* SlackのUnityユーザグループ https://unityuserj-slack-invite.herokuapp.com/
			* アセットストアで購入できるアセットが豊富
			* VGのVR Lab室で記事を書いているので参考にして下さい
* VRコンテンツ開発時の注意点
	* VR酔いを防ぐ
		* FPSを高く保つ
			* 最低でも60~
			* 体感、90あればFPSが原因の酔いは起きづらい
			* FPSが高くてもコンテンツの作りが悪いと酔うことがある
		* 等速移動を心がける
			* 視点の移動に加速があると、身体感覚とのギャップで酔いやすい
				* 人間は速度は感じないが加速度は感じる 
				* 参考) https://www.google.com/design/spec-vr/designing-for-google-cardboard/physiological-considerations.html#physiological-considerations-use-constant-velocity
		* 視野内で更新される情報を減らす
			* 加速時や画面の回転時など、目に入ってくる情報が大きく更新される時に視野を狭めることでVR酔いを軽減出来るという研究結果がある
				* 参考) http://engineering.columbia.edu/fighting-virtual-reality-sickness
	* VRに即したインターフェイスを使う
		* ハンドルコントローラ
			* 主にハイエンドHMDに付属している手で利用するためのコントローラ
			* 自身の手をVR空間上に再現できることで、直感的な動作ができる。また、酔い対策につながるかも？
			* 対応コントローラ
				* Vive Controller
				* Oculus Touch
				* Daydream Controller
		* レティクル
			* 視線で操作するポインター
			* レティクルを表示することで没入感が下がったり、視覚的混乱を招く場合もあるので注意
			* https://www.google.com/design/spec-vr/interactive-patterns/display-reticle.html
		* ヒューズボタン
			* タイマーを使ってアクションを行う時限式ボタン
				* ユーザが数秒見つめたらクリックにする
			* ヒューズボタンはVRコンテンツで市民権を得てきているが、アクションの実行まで待たされるのはストレスに繋がるので注意
			* ヒューズボタン機能を持ったオブジェクトを複数配置する場合、ミスクリックが起きやすいので一定の間隔を空けて置くこと
	* 開発と動作確認のサイクル
		* HMDをつけたり外したりするのが大変
			* 後肩がこる
		* EnvelopVRみたいな、ずっとHMDをつけていられる環境を用意したい
			* あるいは開発者と動作確認者を分ける
* エンジニア募集
