# Procedure Manager（htmlapp-procedures）

単一ファイルのシンプルなHTMLアプリケーションで、手順（ステップ）を準備・管理し、順序に従って実行できる軽量ツールです。サーバ不要で、ローカルにダウンロードしてブラウザで `index.html` を開くだけで動作します。

## 主な機能

- PREPARE（準備）モード：手順の編集、行の追加・削除が可能
- EXECUTE（実行）モード：開始/終了時刻を記録し、順序制御（前のステップが開始/完了していないと次に進めない）
- ステータス遷移：Pending → In Progress → Done（ステータスボタンをクリック）
- CSV インポート/エクスポート（引用符付きフィールド、複数行の引用セルに対応）
- 編集は contenteditable によるインライン編集で簡易操作が可能
- CSVエクスポートはExcel互換のためUTF-8 BOMを付与

## クイックスタート

1. リポジトリをクローンまたはZIPでダウンロード。
2. `index.html` をブラウザで開く（Chrome/Firefox/Edge/Safari 等のモダンブラウザ推奨）。
3. ヘッダーのモードスイッチで PREPARE / EXECUTE を切り替え。
4. "+ ADD STEP" でステップを追加し、Procedure（手順）や Remarks（備考）を編集。
5. EXECUTEモードでステータスを操作：
   - 1回目：Pending → In Progress（開始時刻を記録）
   - 2回目：In Progress → Done（終了時刻を記録）
   - 3回目：Done → Pending（開始/終了時刻をクリア）

## CSVについて

- エクスポート: `EXPORT CSV` で download（columns: ID, Procedure, Status, Start Time, End Time, Remarks）。
- インポート: `IMPORT CSV` でファイル選択。引用符付きフィールドや改行を含むセルに対応する内部パーサを使用。
- ヘッダー行の自動検出（先頭行が "ID" または "Procedure" の場合はヘッダーとして扱う）。
- 列不足の行はスキップされます。

例:
```csv
ID,Procedure,Status,Start Time,End Time,Remarks
1,"作業準備",Pending,,
2,"電源確認",Pending,,
3,"アプリ起動","In Progress","2025/01/01 10:00:00",,"初回実行"
```

## 注意点

- 表示時にIDは自動で再番号付けされます。
- PREPAREモードは手順の編集向け、EXECUTEモードは実行記録向けに操作が制限されます（例：実行中は行の追加/削除が非表示）。
- 実行時の逐次制御により、前のステップがPendingのままだと次のステップを開始できません。

## 拡張案

- JSを外部ファイルへ分離して保守性を向上
- localStorageやサーバ連携で永続化・共有機能を追加
- 多言語対応や印刷用レイアウトの追加

## ライセンス

MIT（必要なら LICENSE ファイルを追加してください）