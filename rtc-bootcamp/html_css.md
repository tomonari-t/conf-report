2018.04.04

## history

以下のポストがAjax時代の幕開け

- [A New Approach to Web Applications](http://adaptivepath.org/ideas/ajax-new-approach-web-applications/)

SPAが流行ったのは、ユーザー時間のうばいが原因。サーバーよりフロントのほうに戦いの戦場がうつった

仮想DOM: メモリ上のDOM。差分更新できますよ

### SSRにおけるクローラーのバージョンについて

- 今はクローラーchroniium41が走ってる
- なのでwebpackのプレフィックサーとかそこいしきして書く必要がある

### Techにおけるフロントコア技術

#### SSR

- JSでレンダリングします

##### BFF

[SSR BFFについて](https://speakerdeck.com/yosuke_furukawa/ssrfalsehua)

#### Isomorphic

[Isomorphic Suvival Guide](https://speakerdeck.com/koichik/isomorphic-survival-guide)

### Atomic Design

[atomic desigh](http://bradfrost.com/blog/post/atomic-web-design/)

### cssセレクタ

詳細度によるセレクタの優先順位が混乱の元。

### BEM

役割や粒度ごとにルールを設けることでルール同士の衝突を避ける設計方針。

- Block: 一意なわかり易い名前
- Element：Blockを構成する要素
- Modifier: BlockまたはElementの表示バリエーションx