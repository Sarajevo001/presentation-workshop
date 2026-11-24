# 複数実行環境対応HTML教材：参照実装 v1.0

- 登録日：2026-11-25
- 技術標準：[実演・演習用HTML教材 技術標準 v1.0](../../guidelines/interactive_html_materials.md)
- 参照元：`Sarajevo001/oop-rpg-workshop`
- 検証・公開済みコードSHA：`3b56de84c6c806a62b985fec9ec33b8518fd30df`
- 参照実装は以下の実ファイルへの固定コミットリンクを正本とする。RPG固有コードを共通リポジトリに複製せず、参照元が変わっても同じ版を取得できる構成にする。新しい汎用テンプレートを検証済みと偽って登録しない。

## 1. 実コード一覧

| 役割 | 検証済み実ファイル |
| --- | --- |
| HTML・環境判定ローダー | [demo.html](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/chapter1/starter/demo.html) |
| CSS | [demo.css](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/chapter1/starter/demo.css) |
| JavaScript（RPG固有の例） | [demo.js](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/chapter1/starter/demo.js) |
| JSFiddleメタ情報 | [demo.details](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/chapter1/starter/demo.details) |
| 旧URL互換 | [index.html](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/chapter1/starter/index.html) |
| 共通ダウンロードUI | [download.html](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/download.html) |
| 共通ダウンロード処理 | [download.js](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/download.js) |
| 教材一覧と導線 | [src/public/index.html](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/index.html) |
| プレゼン内の操作リンク | [chapter4/index.html](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/presentations/chapter4/index.html) |
| 全18ステージ | [examples/](https://github.com/Sarajevo001/oop-rpg-workshop/tree/3b56de84c6c806a62b985fec9ec33b8518fd30df/src/public/examples/) |
| 構造・リンク検査 | [verify_shared_materials.py](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/tests/verify_shared_materials.py) |
| 実ブラウザ検査 | [browser-materials.cjs](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/tests/browser-materials.cjs) |
| 実JSFiddle任意診断 | [check-live-jsfiddle.cjs](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/tests/check-live-jsfiddle.cjs) |
| 章間連続性検証 | [verify_handoffs.py](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/verify_handoffs.py) |
| 既存の機能検査 | [target-contracts.cjs](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/tests/target-contracts.cjs) |
| CI | [validate-target-contracts.yml](https://github.com/Sarajevo001/oop-rpg-workshop/blob/3b56de84c6c806a62b985fec9ec33b8518fd30df/.github/workflows/validate-target-contracts.yml) |
| SHA付き統合制御 | [ci/](https://github.com/Sarajevo001/oop-rpg-workshop/tree/3b56de84c6c806a62b985fec9ec33b8518fd30df/ci/) |

ダウンロードして利用する際はリンク先のRawを選ぶか、次のように固定版を取得する。既存の作業ディレクトリを上書きしない。

```bash
git clone https://github.com/Sarajevo001/oop-rpg-workshop.git rpg-reference
cd rpg-reference
git checkout --detach 3b56de84c6c806a62b985fec9ec33b8518fd30df
```

## 2. 別作品への適用手順

1. 作品で必要な実行環境・配布方法・公開範囲を確定し、本方式の採用可否を判断する。
2. 4ファイルを各教材の内容で構成する。RPGのgame logicは再利用対象外。ローダーの公開ホスト名、メタ情報、CSS/JSの内容を作品に合わせる。
3. download.html/jsを参考に、対象のステージ許容リストとファイル構成を定義する。教材一覧・プレゼン内リンク・JSFiddleのリポジトリ名、ブランチを設定する。
4. 構造検査とブラウザ操作テストの期待値を作品に合わせる。CI runner、Node、ブラウザライブラリ版の互換性と正式承認を確認する。既存の検証は新作品を保証しない。
5. 統合・配備・公開URLの内容比較・代表操作確認を行い、実測と未確認事項を記録する。

## 3. 元実装の再検証手順（読み取り・検証用）

```bash
python3 tests/verify_shared_materials.py
python3 verify_handoffs.py
node tests/target-contracts.cjs
```

上記は構造・既存ロジック・章間検証。ブラウザ自動テストは承認済みの依存・実行環境でCI設定と同じ手順を実行する。Playwright導入を無条件に許可するものではない。実サービスの任意診断は別に実行し、403等で停止する。

## 4. 検証証跡と制約

- [公開版のブラウザCI](https://github.com/Sarajevo001/oop-rpg-workshop/actions/runs/45389049239)：50ケース、既存84アサーション、教材72ファイル。
- [章間連続性CI](https://github.com/Sarajevo001/oop-rpg-workshop/actions/runs/45389049256)：3組×3ファイル。
- [統合安全性CI](https://github.com/Sarajevo001/oop-rpg-workshop/actions/runs/45389049321)。
- [公開・検証完了記録](https://github.com/Sarajevo001/oop-rpg-workshop/blob/f728202071cc3e8827c4099e2ab5e8f6cbe21f52/docs/shared_materials_release_validation_2026-11-24.md)：公開HTTP99ファイルの一致、代表実JSFiddle・公開操作3項目。
- 公開版は実際に動作確認したコードであり、規約全条項への準拠証明ではない。Playwright新規導入の承認証跡・継続利用は [Issue #6](https://github.com/Sarajevo001/oop-rpg-workshop/issues/6) で確認中。
- 実際のVSCode Go Live本体、OS固有フォルダ選択ダイアログの詳細、実JSFiddleの他17ステージ手動確認は未確認。相当環境と代表検証を区別する。自動保存テストはOPFSへの保存である。

## 5. 更新方針

本一覧の固定SHAを変更する場合は、新たな参照版の変更内容と検証証跡を確認し、変更理由を記録する。参照コードの機械的複製・改変版の無検証採用を行わない。
