# 付録E：Windows固有の注意点

この教材はWindows環境を対象としています。
Windows環境でPython開発を行う際の注意点や、よくある問題とその対処法をまとめています。

---

## 目次

1. [コマンドの基本](#コマンドの基本)
2. [ショートカットキー](#ショートカットキー)
3. [パスの記法](#パスの記法)
4. [ターミナル・シェル](#ターミナルシェル)
5. [よくある問題と対処法](#よくある問題と対処法)

---

## コマンドの基本

### ファイル・ディレクトリ操作

| 操作 | コマンド | 例 |
|------|---------|---|
| ディレクトリ一覧 | `dir` | `dir` |
| 現在のディレクトリ表示 | `cd` | `cd` |
| ディレクトリ移動 | `cd パス` | `cd C:\Users\username\Documents` |
| ディレクトリ作成 | `mkdir フォルダ名` | `mkdir myproject` |
| ファイル削除 | `del ファイル名` | `del test.txt` |
| ディレクトリ削除 | `rmdir /s フォルダ名` | `rmdir /s myproject` |
| ファイル内容表示 | `type ファイル名` | `type data.csv` |
| 画面クリア | `cls` | `cls` |
| ファイルコピー | `copy 元 先` | `copy a.txt b.txt` |
| ファイル移動 | `move 元 先` | `move a.txt folder\` |

### ファイル検索

**テキスト検索：**
```bash
# ファイル内の文字列を検索
findstr "検索文字列" ファイル名

# 例：pandasという文字列を検索
conda list | findstr pandas
```

**ファイル名検索：**
```bash
# サブディレクトリを含めて検索
dir /s ファイル名

# 例：すべての.pyファイルを検索
dir /s *.py
```

### 環境変数

| 操作 | 書き方 | 例 |
|------|-------|---|
| 環境変数表示 | `echo %変数名%` | `echo %USERPROFILE%` |
| ユーザーフォルダ | `%USERPROFILE%` | `C:\Users\username` |

**例：ホームディレクトリへ移動**
```bash
cd %USERPROFILE%
```

---

## ショートカットキー

### VS Code

| 操作 | ショートカット |
|------|--------------|
| コマンドパレット | `Ctrl + Shift + P` |
| ファイルを開く | `Ctrl + O` |
| 保存 | `Ctrl + S` |
| すべて保存 | `Ctrl + K` → `S` |
| ターミナル表示 | `` Ctrl + ` `` |
| コピー | `Ctrl + C` |
| 貼り付け | `Ctrl + V` |
| 切り取り | `Ctrl + X` |
| 元に戻す | `Ctrl + Z` |
| 検索 | `Ctrl + F` |
| 置換 | `Ctrl + H` |
| セル実行（Jupyter） | `Shift + Enter` |

### ターミナル内

| 操作 | ショートカット |
|------|--------------|
| プロセス中断 | `Ctrl + C` |
| コピー（選択後） | `Ctrl + C` または 右クリック |
| 貼り付け | `Ctrl + V` または 右クリック |

---

## パスの記法

### Windowsのパス表記について

Windowsでは、エクスプローラーやコマンドプロンプトでパスを表示すると `\` (バックスラッシュ) で区切られています。

**例：エクスプローラーやコマンドプロンプトでの表示**
```
C:\Users\username\Documents\python_projects\myproject
```

**重要：** しかし、Pythonコード内では `\` をそのまま使うとエラーになります。

### Pythonでのパス指定

Pythonコード内でパスを書く場合、以下の3つの方法があります。

```python
# 方法1：スラッシュを使う（推奨）
path = "C:/Users/username/Documents/data.csv"

# 方法2：rawストリング（r を付ける）
path = r"C:\Users\username\Documents\data.csv"

# 方法3：バックスラッシュを2つ書く
path = "C:\\Users\\username\\Documents\\data.csv"
```

**推奨：** 方法1（スラッシュ `/` を使う）が最も読みやすく、エラーが少ない。

**NG例：**
```python
# これはエラーになる
path = "C:\Users\username\Documents\data.csv"  # \U, \D などが特殊文字として扱われる
```

### ホームディレクトリ

**コマンドライン：**
```bash
# 環境変数を使う
cd %USERPROFILE%
```

**Pythonでの取得：**
```python
import os

# ホームディレクトリを取得
home = os.path.expanduser("~")
print(home)
# 出力例：C:\Users\username
```

### 絶対パスと相対パス

```python
# 相対パス
"data/sales.csv"
"../output/result.txt"

# 絶対パス
"C:/Users/username/project/data.csv"
```

### OSに依存しないパス処理（推奨）

```python
import os

# パスを結合（OSに依存しない）
path = os.path.join("data", "sales.csv")
# Windows: data\sales.csv

# カレントディレクトリ
current = os.getcwd()
```

---

## ターミナル・シェル

### Windowsのターミナル種類

**種類：**
- **コマンドプロンプト (cmd.exe)** - 標準
- **PowerShell** - 高機能版
- **Anaconda Prompt** - conda専用（推奨）

### Anaconda Promptの起動

**起動方法：**
1. Windowsキーを押す
2. 「Anaconda Prompt」と入力
3. 「Anaconda Prompt (miniconda3)」を選択

**プロンプト表示：**
```
(base) C:\Users\username>
```

### 初期化コマンド

VS Codeでcondaを使う場合、初回のみ実行：

```bash
# コマンドプロンプトの場合
conda init cmd.exe

# PowerShellの場合
conda init powershell
```

その後、VS Codeを再起動。

---

## よくある問題と対処法

### 問題1：「Windows Defender SmartScreen」の警告

**症状：** Minicondaインストール時に警告が出る

**解決方法：**
1. 「詳細情報」をクリック
2. 「実行」をクリック
3. 公式サイトからダウンロードした場合は安全です

### 問題2：日本語の文字化け

**症状：** コマンドプロンプトで日本語が文字化けする

**解決方法：**
```bash
# UTF-8に変更
chcp 65001
```

または、VS Codeのターミナルを使う（推奨）

### 問題3：「python」と入力するとMicrosoft Storeが開く

**症状：** `python` コマンドでMicrosoft Storeが起動する

**解決方法：**
1. 「設定」→「アプリ」→「アプリと機能」
2. 「アプリ実行エイリアス」をクリック
3. 「アプリインストーラー python.exe」をオフにする

または、Anaconda Promptを使う（推奨）

### 問題4：ファイルパスにスペースや日本語

**症状：** `C:\Users\山田 太郎\Documents` のようなパス

**影響：** エラーの原因になる可能性

**対策：**
```python
# パスを引用符で囲む
path = "C:/Users/山田 太郎/Documents/data.csv"

# または、rawストリングを使う
path = r"C:\Users\山田 太郎\Documents\data.csv"
```

**推奨：** プロジェクトフォルダは英数字のみの場所に作成

### 問題5：conda コマンドが認識されない

**症状：** 「'conda' は、内部コマンドまたは外部コマンド...」

**解決方法：**
- **通常のコマンドプロンプトではなく、Anaconda Promptを使う**
- VS Codeの場合は `conda init cmd.exe` を実行して再起動

### 問題6：VS Codeのターミナルでcondaが使えない

**症状：** VS Code内のターミナルで conda コマンドが動かない

**解決方法：**
```bash
# 初期化（初回のみ）
conda init cmd.exe

# VS Codeを再起動
```

---

## Minicondaインストール時の注意点

### インストールオプション

Minicondaをインストールする際：

**推奨設定：**
- 「Just Me」を選択
- 「Add to PATH」は**チェックしない**（Anaconda Promptを使うため）
- 「Register as default Python」にチェック

### インストール後の確認

```bash
# Anaconda Promptを起動して確認
conda --version

# 出力例：conda 24.1.2
```

---

## VS Code設定のヒント

### ターミナルの設定

VS Codeのターミナルでcondaを快適に使うために：

1. VS Codeを開く
2. ターミナルを表示（`` Ctrl + ` ``）
3. 初回のみ、Anaconda Promptで実行：
   ```bash
   conda init cmd.exe
   ```
4. VS Codeを再起動

これで、VS Codeのターミナルで直接condaコマンドが使えるようになります。

### 改行コードの設定

**確認方法：**
- 右下のステータスバーに「CRLF」と表示される
- これがWindowsの標準改行コード

**変更方法：**
- 右下の「CRLF」をクリックして選択可能
- 通常は「CRLF」のままでOK

---

## トラブルシューティングチェックリスト

Python開発でエラーが出た時、以下を順番に確認：

1. **Anaconda Promptを使っているか？**
   - 通常のコマンドプロンプトではcondaが動かない

2. **conda環境はアクティベートされているか？**
   ```bash
   conda env list
   # * がついている環境が現在アクティブ
   ```

3. **プロンプトの表示を確認**
   ```bash
   (myproject) C:\Users\username>  # OK
   (base) C:\Users\username>       # base環境（注意）
   ```

4. **パスに日本語やスペースが含まれていないか？**
   - プロジェクトフォルダ名は英数字のみを推奨

5. **VS Codeのインタープリタは正しい環境を選択しているか？**
   - 右下のステータスバーで確認
   - 間違っている場合はクリックして選択

---

## まとめ

### Windows環境での重要ポイント

1. **Anaconda Promptを使う**
   - 通常のコマンドプロンプトではなく、必ずAnaconda Promptを使用

2. **パスはスラッシュ `/` を使う**
   - Pythonコード内では `C:/Users/username/...` と書く

3. **プロジェクトフォルダは英数字のみ**
   - 日本語やスペースを含むパスは避ける

4. **環境をアクティベートする**
   - プロンプトの `()` 内を確認してから作業

5. **VS Codeのターミナルは初期化が必要**
   - `conda init cmd.exe` を実行して再起動

### よく使うコマンド（Windows版）

```bash
# ディレクトリ一覧
dir

# 現在のディレクトリ
cd

# ディレクトリ移動
cd C:\Users\username\Documents

# パッケージ検索
conda list | findstr pandas

# 画面クリア
cls
```

---

**目次に戻る：** [第0章：目次](./第0章_目次.md)
