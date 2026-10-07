# SIXTYZERO ステータス

## [📈 ステータスページ](https://status.sixty-zero.app): <!--live status--> **すべて正常に動いています**

SIXTYZERO(sixty-zero.app)の稼働状況と、障害・メンテナンスのお知らせを出すリポジトリ。[Upptime](https://upptime.js.org) で動いている(GitHub Actions が 5 分ごとに外から確認し、GitHub Pages でページを出す)。設定は `.upptimerc.yml` だけ。`.github/workflows/` は Upptime が毎週書き直すので手で直さない。

<!--start: status pages-->
<!--end: status pages-->

## 告知の書き方(運営)

告知は Issue で出す。**ステータスページに出るのは、運営がラベルを付けた Issue だけ。** テンプレートにはラベルを入れていない(誰でも Issue を作れる公開リポジトリなので、テンプレート経由で外部の人が告知を出せないようにしている)。

### 障害のお知らせ

1. 「New issue」→「障害のお知らせ(運営用)」で作る。題名と本文は日本語で書く。
2. ラベル `status` **だけ**を付ける(`site` などの監視の名前のラベルは付けない。付けると、その監視が戻ったときに自動で閉じられる)。
3. 外部の人がコメントできないよう、右の欄の「Lock conversation」で鍵をかける。
4. 続報はコメントで足す(コメントもステータスページに出る)。解決したら最後に原因と対応をコメントし、Issue を閉じる。

- 作ってから 15 分以内に閉じ、コメントが 1 件だけの `status` の Issue は、Upptime が誤検知とみなして**削除する**。短い障害の記録を残すときは、コメントを 2 件以上にするか 15 分以上たってから閉じる。
- 監視が「停止」を見つけたときは Upptime が自動で Issue を作る(題名と本文は英語で固定。`nowex35` が担当に付き、鍵もかかる)。説明はその Issue にコメントで足す。題名を日本語に変えてもよいが、「低下」の Issue は題名の `degraded` で黄色く表示しているので、その語が消えると赤の表示になる。

### メンテナンスの予告

1. 「New issue」→「メンテナンスの予告(運営用)」で作る。
2. 本文の**先頭**の `<!-- -->` の中を書き換える(本文で最初の `<!--` だけが読まれる)。
   - `start` / `end`:開始と終了の日時。`+09:00` を付けて日本時間で書く。
   - `expectedDown`:この間に止まると分かっている監視の名前(slug)を , 区切りで。今あるのは `site`。`api` は「アプリ・API」を有効にした後に使える。遅くなるだけなら `expectedDegraded`。
3. ラベル `maintenance` を付け、鍵をかける。
4. `end` を過ぎると Upptime が自動で閉じる。`expectedDown` に書いた監視は、この間に止まっても障害の Issue が作られない。

## 監視している項目

| 表示名 | slug | 測る URL | 正常の条件 |
| --- | --- | --- | --- |
| サイト(sixty-zero.app) | `site` | `https://sixty-zero.app/.well-known/security.txt` | 200 で本文に `Contact:` がある |
| アプリ・API(未有効) | `api` | `https://sixty-zero.app/api/health` | 200 で本文に `"backend":"ok"` がある |

「アプリ・API」は `/api/health` が本番に出てから `.upptimerc.yml` のコメントを外して有効にする。

## ライセンス

- 仕組み:[Upptime](https://github.com/upptime/upptime)
- コード:[MIT](./LICENSE)
