# Nauts Event #01

[Nauts ホバー大喜利](https://note.com/nautsdc/n/n2c66da8cb510)のプロジェクトです

## セットアップ

```bash
npm install
npm run dev
```

`http://localhost:4321` で確認できます。

| コマンド | 説明 |
| --- | --- |
| `npm run dev` | 開発サーバーを起動 |
| `npm run build` | `dist/` に静的ファイルを出力 |
| `npm run preview` | ビルド結果をローカルでプレビュー |

## ディレクトリ構成

```
src/
  components/
    Header.astro       ロゴ・ナビゲーション・Contactボタン
    MemberCard.astro    メンバー1人分のカード(写真・肩書き・捕食インタラクション)
    Footer.astro        フッター(未使用・現在ページには非表示)
  data/
    members.js          メンバー情報(会社名・氏名・肩書き・顔の位置)
  layouts/
    BaseLayout.astro     共通レイアウト + 捕食インタラクションのロジック一式
  pages/
    index.astro          メンバー一覧ページ
  styles/
    global.css            全体のリセット・カラー・フォント
public/
  images/members/         メンバー写真
  images/nauts-logo.svg   ロゴ
```

## メンバーを追加・編集する

`src/data/members.js` に1オブジェクト追加すればOKです。

```js
{
  company: '会社名',
  name: 'Full Name',
  roles: ['役職1', '役職2'],
  photo: 'photo-filename.png', // public/images/members/ に配置
  face: { x: 50, y: 40 },      // 写真内の顔の位置(%)。目・口の表示位置に使う
}
```

写真は `public/images/members/` に追加してください。`face.x` / `face.y` は写真の左上を(0,0)、右下を(100,100)としたときの目の中心位置の目安です。

## カーソルを食べる

各写真にカーソルを近づけると:

1. 写真に薄く仕込まれた目と口が現れる
2. しばらく粘るとカーソルを追いかけ始め、捕食する(効果音あり)
3. 満腹になるとお腹が少し膨らみ、マウスの動きに合わせて揺れる
4. 写真をクリックすると「ぺっ」と吐き出す。吐き出された直後のカーソルはしばらくベタつく

音のオン/オフは右下の🔊ボタンから切り替えられます。ロジックは `src/layouts/BaseLayout.astro` 内の `<script>` にまとまっています。
