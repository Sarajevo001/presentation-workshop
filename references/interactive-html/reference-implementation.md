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
- 公開版は実際に動作確認したコードであり、規約全条項への準拠証明ではない。Playwright 1.56.1 / Chromium の継続利用は2026-11-25に承認済み（[Issue #6](https://github.com/Sarajevo001/oop-rpg-workshop/issues/6)）。新規導入時の事前承認証跡、保守・セキュリティ・ライセンスの詳細確認は未完了。新規依存や版変更の包括承認ではない。
- 実際のVSCode Go Live本体、OS固有フォルダ選択ダイアログの詳細、実JSFiddleの他17ステージ手動確認は未確認。相当環境と代表検証を区別する。自動保存テストはOPFSへの保存である。

## 5. 更新方針

本一覧の固定SHAを変更する場合は、新たな参照版の変更内容と検証証跡を確認し、変更理由を記録する。参照コードの機械的複製・改変版の無検証採用を行わない。

## 6. 講座入口の分離と素材掲載の追加参照例（2026-11-27登録）

既存のv1.0固定参照版は変更しない。以下は別の後続版の追加参照例であり、旧版の公開99ファイル一致を新しい版の証跡として扱わない。

- 対象SHA: `f2dfad330c05e071a55236a0d616a3f81c71ad59`（RPG講座）。[講義入口](https://github.com/Sarajevo001/oop-rpg-workshop/blob/f2dfad330c05e071a55236a0d616a3f81c71ad59/src/public/index.html)、[教材一覧](https://github.com/Sarajevo001/oop-rpg-workshop/blob/f2dfad330c05e071a55236a0d616a3f81c71ad59/src/public/materials.html)、[看板PNG](https://github.com/Sarajevo001/oop-rpg-workshop/blob/f2dfad330c05e071a55236a0d616a3f81c71ad59/src/public/assets/xo-code-busters-banner.png)、[総まとめ](https://github.com/Sarajevo001/oop-rpg-workshop/blob/f2dfad330c05e071a55236a0d616a3f81c71ad59/src/public/presentations/summary/index.html)、[ブラウザ検査](https://github.com/Sarajevo001/oop-rpg-workshop/blob/f2dfad330c05e071a55236a0d616a3f81c71ad59/tests/browser-materials.cjs)。
- 統合後CI: [表示・操作・教材検証](https://github.com/Sarajevo001/oop-rpg-workshop/actions/runs/45828155079)、[章間検証](https://github.com/Sarajevo001/oop-rpg-workshop/actions/runs/45828155162)、[統合検証](https://github.com/Sarajevo001/oop-rpg-workshop/actions/runs/45828155127) は合格。PC・狭幅表示の検査と看板の原本一致検査を含む。
- 共通玄関は公開基盤側の [XO-Code Bustersの固定参照版](https://github.com/Sarajevo001/xo-code-busters/blob/30ae57aa8cd30f2150c73e7aa31da36f55d2734f/src/public/demo-portal/index.html)。RPGの配備定義を変更せず、XO側でルートを追加した。[統合後CI](https://github.com/Sarajevo001/xo-code-busters/actions/runs/45832165655) は合格。
- 2026-11-26、作成者のVPS実行ログでCaddy設定の検証・適用成功を確認。ユーザーの実ブラウザ画面で共通玄関・講座トップ・看板の表示と遷移を確認。2026-11-27、ユーザーが全編確認の上、教材制作をいったん完成と判断。新しい版の公開HTTP全ファイル比較、全非公開パスの拒否確認、講座所要時間の実測はこの証跡では確認していない。
