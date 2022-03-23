# 脱DVAの方針とか諸々

今回トライするミッションについて諸々書く。プロジェクト計画書的な立ち位置の文書



## 現状のSDB-FRONTの課題

#### 課題

1. TypeScriptとJavaScriptが混在する

2. フレームワークが古い（Dva依存ライブラリが古くUnitテストが書きづらい）

3. ライブラリの重複（同じ用途のライブラリを入れてて無駄が多い）

4. UNITテストがない

   

#### 詳細

###### 1.TypeScriptとJavaScriptが混在する

TypeScriptにするメリットとして、SDBの持つ巨大なJSON Responseを型で整理できるというのがある。もともとSDBのResponseはJAVAでつくられており型前提で帰ってくる値なので、TypeScriptとの相性は悪くない。型がつくことで、コードの見通しがよくなり、IDEの機能をフル活用出来る。結果として、新しくJOINしたメンバーに対する教育的メリットが出やすい。また、言語的に、TypeScriptは最終的にJavaScriptにConvertされて動くので混在していても動作に問題はないので、徐々に着手ができる。とはいえ共通クラスの整理は必要。



###### 2.フレームワークが古い

Dvaの依存ライブラリが古い

- Dva自体のメンテナンスが2年前にストップしてる。依存ライブラリもdeprecatedの物が多い
- ReactRouterがV4まま。Reduxバージョンも古い
- 現状のSmartDB構成でDvaに頼る必要は特にない。
- 中国製のライブラリが日本市場において嫌われる可能性があるし、国際関係どうなるかよくわからん



###### 3.ライブラリの整理

そもそも別チームで動いてたのである程度仕方ない。とはいえそんなに致命的なものがあるわけではない。この機に整理したいというだけ。



###### 4.UNITテストがない

そもそも無い、というのが今どきありえないし、このままではSaaSサービスのリリース速度についていけなくなる可能性が高い。テスターの負荷、コストがかかったままになる



## 課題解決の方法

Dvaを完全に撤廃し、代わりにRedux-ToolKit+connected-react-router+TypeScript+axiosを使おうと思います。

ReduxToolKit（以下RTK）を選定した理由は以下の通りです。

・Reduxよりコードの可読性がよくシンプル。公式でも推奨されてる
・Dvaとおおよそ同じことができる
・TypeScriptでメンテナンス＋コード品質あげられる
・DVaもReduxベースなのでアーキテクト構造は基本同じ

実際にPoCでダッシュボードを置き換えてみたところ特に問題なかったので、この方向でいこうと思います。
ただ、PoCをやってみてわかった課題もあります。以下の通り。

- Routing：移行の問題はない。ただし機能毎に徐々に移行するのは難しい。やるなら一気に。
- 状態管理：移行の問題はない。現状のState管理は整理は必要。あと性能面は未検証。
- 非同期通信：何を選択するか未だに迷い中。世の中の流れ的にはSagaでもThunkでもなくHooksっぽいが。
- tsとjsの混在：特に問題なし。混在してても動くし、既存のUtilクラスもある程度使える。とはいえUtilはTS化したい。



## POCの結果について

技術選定＋SDB構造把握＋Redux把握（ダッシュボードまで）で3週間程度。ダッシュボードの置き換えは概ね4日ほど掛かったが、置き換え自体は可能と判断できた。

PoCの結果を踏まえた基本方針を以下の通り。

1. RTK＋thunk or Hooksで非同期通信

2. Stateは基本RTKのSlice使う

3. できるだけTs化してStateのInterfaceを明確にする

4. 通信はAxios（エラー処理とか楽だし）

5. Redux-sagaはやめる。（modelと一体化しすぎてしんどい）

6. Fetchはやめる（冗長だしテスト書きづらい）

7. Dva抜く（既定路線）

   

## 全体の手順

1. とりあえず以下をインストール。
   reduxjs/toolkit": "^1.5.0",
   axios": "^0.21.1",
   connected-react-router": "^6.8.0",
   react-redux": "^7.2.2",
2. Redux-toolkitの作法を学ぶ。まずCreateSliceを学ぶ。
3. DVaRouterを置き換える。
   history作ってconnectRouter(history)でComineReducersしてConfigureStoreにMiddleWareとして渡せばいけるっぽい。
   拡張してるLayoutのところは少し工夫が必要。
4. axiosを使った非同期通信を実装する。
   新しく作った部分はTypescript化している。旧版のUtilは使えないので使ってない。
5. Reloginを置き換える
6. ヘッダを置き換える
7. サイドメニューを置き換える
8. ダッシュボードを置き換える



## 具体的な手順

1. 既存のmodel/xxxx　がAPI呼び出しなので、これはxxxAPI.tsとしてっ純関数に切り出す

   model >>> Store/Slice配下にしてCreateSlice化
   Action部分の一部はStore/Api配下に切り出す
   １）yield callしてるやつをAPIに切り出す。ThunkAction作る。Sliceの元ネタ
   ２）yield put してるやつがStateなのでInterfaceつけてStateにする。これもSliceの元ネタ

   

2. 既存のcomponent/xxxx はDOMと関数呼び出しを担当してるので、DOMの部分はそのままで、関数呼び出しの部分dispatch,stateの値を取得する部分をそれぞれuseDispatch,useSelectorに置き換えれば影響なく動くはず。
   component >>> DOM前の処理をuseSelectに置き換え。
   DOMは変更しない。JSのままでいい。

3. 既存のroute/xxxもDOMと関数呼び出しを担当してるので、pagesに相当。できればTSにしたい。dispatchしてるところを,UseDispatchに置き換え。Propsのバケツリレーが多いんだけどなんでですか？１）dispatch({ type: 

   "topLayout/deleteSearchHistory", keyword: keyword })の形でdispatchされるので、
   呼び出しのタイミングでuseDispatch()に変更。呼び出しタイミングは考えた方が良さそうに見える。

4. util >>> requestはaxiosのやつに変換。使えるやつはそのまま使う？全般TS化したほうが使いやすそう。



## リスク

1. mobileが1番大変そう。以前に対応したときに不具合がでて大変だった。またやると思うと。。。：4月からDLSさん利用

2. TypeScriptの学習コストが必要

3. 動作している既存の機能に影響を与えないようにする必要がある

4. テスターのコストが掛かる

5. DVaで実現していた機能を完全に置き換えられるか不明な点がある

6. RTKを使ったテスト記述方法はまだ未学習（世の中的には絶対ノウハウあるはず）

   

## リスク解決手法

モブプロとUNITテストの記述

を実施することで上記のリスク解決を目指す。

1日2時間のモブプロ4人（夏、井上、久冨、李）で実施、全員の知見とノウハウの共有を目指す。



## ブランチ戦略について

4月以降で予定されてるもの
新フォーム　バグ修正とか細かい機能追加　>>　 topic/ >5.1にマージ
					 　大物レイアウトブロック権限とか  >>　 newform/ >5.1にマージ（ちょっとマージ大変）多分あんまりない
SDB本体のバグ修正とか機能追加　>>　 topic/ > 5.1にマージ
脱Dvaの作業　>>　 escdva/ > 5.1にマージ（マージが大変） 毎日Rebase担当決めてモビングの後escdvaを最新の5.1でRebaseし、最後に一気にマージする際の事故を防ぐ。

基本はNewForm関連の修正プルリクはTopicに格上げする感じ。
これまでのNewFormの扱いと同じになるのがescDva配下のブランチとなる。

	5.1	
	+ topic/ いままでと同じ。新フォームの細かい修正もここにいれる
	
	+ newform/ 大きい新フォーム用（あんまり作りたくないけど）
	
	+escdva/dev こまめに5.1Rebase >> sdbpocにイメージがあたってる
	  + escdva/worklist	機能ごとにブランチを作る
	  + escdva/favorite
	  + escdva/dashboard
	  + escdva/mobile



---



### モブプロの目的はなに？

教育、実装、知見共有の3つを1石3鳥したい。



### モブプロで何の作業をするのか？

脱Dva作業をやります。

脱Dva作業とは端的に言うと、

- ReduxToolKit導入
- ReactRouterV5導入
- TypeScriptの導入
- リファクタリング

です。この作業の目的はSDB-Frontメンテナンスコスト削減とCI/CD化です。

（機能的にいうなら別に脱Dvaする必要ないのにあえてやるのは上記の目的があるからです）

### モブプロの進め方は？

一般的なモブとタイピストパターンでやります。モブとタイピストという2つの役割があって、時間制で持ち回りのタイピスト1人と、その他全員がモブになるやつです。詳細は別途。

### 使うツールは？

VisualStudioCodeのLiveShare＋Discordを使います。Teamsは重たいので、画面共有はLiveShare、音声はDiscordでやります。



### 大事なこと

#### HRT（謙虚・尊敬・信頼）の原則

相手を否定・非難してはいけません。HRTは、謙虚・尊敬・信頼を意味する略語です。お互いHRTの原則で仲良くやりましょう。



参考

https://note.com/erukiti/n/nd14df57c4312





Request.js 



2021/04/07

脱Dva作業の予定

昨日



管理者のおすすめバインダ､お気に入りバインダ

Escdva/#927-admin-recomend



ユーザーテスト



スムーズ

瞬殺(しゅんさつ)

辿る(たどる)摸索前进，探索，追踪

Uses tae 



Input. value state onChange 