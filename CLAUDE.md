# CLAUDE.md — pc-sleep-guard（PCスリープガード）

> 横断の前提は **`oikawa3673/scm-renkei-hub`** が正本（`外付けアプリ開発の前提.md`・`横断ノウハウ/リポジトリ衛生.md`）。
> これは TCloud for SCM の外付けアプリではなく、社内向けの**小さな Windows 常駐ツール**（C# 1ファイル）。
> 使い方・ビルド方法は `README.md`、今どこまでかは `HANDOFF.md`。

## 守ること

- 文字コードと改行を変えない: `.cs` は **BOM付きUTF-8**、`.bat` / `.vbs` は **Shift-JIS＋CRLF**（`.gitattributes` の `-text` を外さない）。
  エディタやスクリプトで保存し直すと壊れる
- **配布物（exe・zip）は GitHub Release へ**。新しくコミットしない（`.gitignore` 済み）。既存の追跡ファイルの削除・履歴の書き換えはユーザー判断
- ソースに個人のフォルダの絶対パスを書かない（`$PSScriptRoot` や引数で渡す）
- ONの間は自動ロックが効かない。この注意書きを画面・README から消さない

## 検証

Windows なら README の csc コマンドでビルドして起動・ON/OFF・トレイ・二重起動を触る。
Linux では `mcs -target:winexe -win32icon:_作業ファイル/app.ico -r:System.dll -r:System.Drawing.dll -r:System.Windows.Forms.dll _作業ファイル/SleepGuard.cs` でコンパイルが通ることまで確かめられる（動作確認はできない）。
