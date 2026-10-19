# BrowserDeck site rules

BrowserDeck(iOSのブラウザ)が使う、サイト別のルールの配信物です。

- `rules.json`: ルールの本体(人が読み書きする)。
- `site-rules.json`: アプリが取りに来る配信物。`{"payload": rules.jsonのBase64, "signature": Ed25519署名のBase64}`。

アプリは署名・形式・期限・対象のアプリの版・**今より新しい版か**を確かめてから使います。
ルールはデータだけで、決まった操作(横の端まで送る・叩く・焦点を当てる・隠す)しか表せません。
スクリプトは含みません。アプリから送る情報はありません(このファイルを取りに来るだけ)。

## 更新のしかた

1. `rules.json`を直し、`version`を前回より大きくする(アプリ同梱の版より大きい物だけ取り込まれる)。
2. 手元で署名する(署名鍵はこのリポジトリには置かない):

   ```sh
   swift <iPadKeyboard>/BrowserDeck/Tools/site-rules.swift sign <秘密鍵> rules.json site-rules.json
   ```

3. 2つのファイルをコミットして`push`する。GitHub Pagesが数分で公開する。
   端末は1日1回まで取りに来て、アプリを次に開いた時から効く。

公開先: https://toyprogram.github.io/browserdeck-site-rules/site-rules.json
