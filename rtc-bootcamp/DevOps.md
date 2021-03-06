# DevOps

## What Service Operatoin

ソフトにおけるシステムのコストの40-90%はシステムの誕生後によって生じるから保守は大事。

定型業務と非定型業務に別れる。

定型業務はツール化して自動化を。非定型業務はそれをみすえて設計

### 定型業務

以下３つの業務が行われることがおおい。

#### 環境維持

複数ある開発環境をリリース後に整備する。これむずいよね。

複数案件走っていて、取り込みたいとか取り込みたくないとか。

#### リリース

案件を世に公開する業務

#### 監視モニタリング

そのまんま。見える化ツールとか導入しよう。

**見える化ー＞標準化ー＞自動化**のステップで自動化を行う。

### 非定型業務

突発的に発生。定型化しにくいが過去の知見を活かしながら実施していく必要がある。

障害対応や問い合わせ調査などがそれにあたる。

対応できるように事前に設計することが大切。

#### 性能設計

想定アクセス数。それに基づくマシン台数。性能劣化を防ぐ。

#### ログ設計

出力項目の定義と、エラー特定のキーワードをきめる。障害発生時に原因をつかめるようにする。

#### ディレクトリ設計

アプリが配置される先やログ出力される先の定義と各ディレクトリのオーナーを決める。誰でも手軽にいじれるような環境を作る。

## ハンズオン

- SQLなどのWhat causeがログとセットであれば良い。
- 1Sessionで判断できるようになりたい。ユーザー検索できるように
- タイムの表示は厳格に揃える
- リクエスト情報が少ない
- バラバラのログではなく一貫してlog管理が行う基盤が必要
- 入り口から出口まで一貫して
- **再現可能な情報を載せる**


### 甲矢さんが考えるログに出すべき情報!!

1. ユーザーの行動を特定するためのコードをHTTP-HECDER。SSIDだと使いまわされる可能性があるため、「ハッシュ値＋ホスト名」がのぞましい。APサーバー側でヘッダー付与しよう。

2. ミリ秒までログ出力しよう

3. サーバーで受け取ったパラメーターやIPを項目を出力。個人情報の出力。プロキシ・サーバーとか立てているときは`X-Fowarded-For`に本元のIPを収めておかないとIPアドレスきえちゃうので注意。

4. エラー発生時にはエラーコードを出力(UIに)する。各コードに対する意味付け(ユーザ操作か、サーバ起因か、どんな内容か、等)を事前に行い出力する。

**特定をいかにじんそくにできるかのログ設計が大切。**

## At R

領域担当と領域横断担当とでポリシーが変わってくる。

サービスの成長にともなってシステムの大規模化。初期段階でそうていしていたリリース方式は陳腐化し、アドオンの要素が増えることでリリースという作業の負荷が増加してしまう。

成長すると体制も変化する。その変化を見据えた仕組みを作る必要がある。リリース自体の自動化を目的とせず、リリース対象と作業両方のコード化・構成管理を行う必要がある。


## システムのコード化とは

構成管理を取り込んだリリースであること
各サブシステム間のリリースに対応する依存関係を
本番と開発の差分を吸収する
スケールが容易であること

### 構成管理とは

**構成管理とはリポジトリによる一元化と、環境情報とコードの分離ができた状態で管理すること。**

ソース自体の管理

テストスクリプトの管理

環境情報の管理

これらを合わせてリリース実行すること

#### 技術選定

すべてが一元化さている必要がある。そのため、技術的な先進性よりもエンジニアの手に馴染む技術要素を選択する必要がある。**利用し続けてもらうことが大切。**

#### 環境依存の分離

環境に依存する情報とコードを分離して管理できる必要がある。コード一元化のため

#### テストスクリプト

テストを自動化して、品質とスピードを維持するべき。いつでもテスト可能とするために、コードと合わせて管理するべき。

#### 責任範囲の切り分け

構成管理対象を一つに仕組みでやろうとすると破綻する。**それぞれはシンプルに、それぞれの対象にあったツール（アンシブルとか独自ツールとか）それらをJenkinsなどでオーケストラレーションを行いリリースするなどする。(Kabukuもそうだった)**


リリースのDBにおける冪等性（繰り返ししても同じ処理が含まれる）。普通、DBのPUTすると冪等性なくなる。それをLiquibaseでやると、DBの履歴が残っており、繰り返しやるとスキップしたりできるきのうがある。

冪等性大事だなぁ。