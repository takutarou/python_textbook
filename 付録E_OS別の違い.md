# 付録E：OS別の違い（Windows中心）

この教材は主にWindows環境を対象としていますが、Mac環境と異なる部分をまとめています。
チーム内でMacユーザーがいる場合の参考にしてください。

---

## 目次

1. [コマンドの違い](#コマンドの違い)
2. [ショートカットキーの違い](#ショートカットキーの違い)
3. [パスの記法の違い](#パスの記法の違い)
4. [ターミナル・シェルの違い](#ターミナルシェルの違い)
5. [インストール手順の違い](#インストール手順の違い)
6. [よくある環境固有の問題](#よくある環境固有の問題)

---

## コマンドの違い

### ファイル・ディレクトリ操作

| 操作 | Windows | Mac/Linux |
|------|---------|-----------|
| ディレクトリ一覧 | `dir` | `ls` |
| 現在のディレクトリ表示 | `cd` | `pwd` |
| ディレクトリ移動 | `cd パス` | `cd パス` |
| ディレクトリ作成 | `mkdir フォルダ名` | `mkdir フォルダ名` |
| ファイル削除 | `del ファイル名` | `rm ファイル名` |
| ディレクトリ削除 | `rmdir /s フォルダ名` | `rm -r フォルダ名` |
| ファイル内容表示 | `type ファイル名` | `cat ファイル名` |
| 画面クリア | `cls` | `clear` |
| ファイルコピー | `copy 元 先` | `cp 元 先` |
| ファイル移動 | `move 元 先` | `mv 元 先` |

### ファイル検索

| 操作 | Windows | Mac/Linux |
|------|---------|-----------|
| テキスト検索 | `findstr 文字列 ファイル名` | `grep 文字列 ファイル名` |
| ファイル名検索 | `dir /s ファイル名` | `find . -name "ファイル名"` |

**例：conda listでpandasを検索**

```bash
# Windows
conda list | findstr pandas

# Mac/Linux
conda list | grep pandas
```

### 環境変数

| 操作 | Windows | Mac/Linux |
|------|---------|-----------|
| 環境変数表示 | `echo %変数名%` | `echo $変数名` |
| ユーザーフォルダ | `%USERPROFILE%` | `~` または `$HOME` |
| パス区切り | `;` | `:` |

**例：ホームディレクトリへ移動**

```bash
# Windows
cd %USERPROFILE%

# Mac/Linux
cd ~
```

---

## ショートカットキーの違い

### VS Code

| 操作 | Windows | Mac |
|------|---------|-----|
| コマンドパレット | `Ctrl + Shift + P` | `Cmd + Shift + P` |
| ファイルを開く | `Ctrl + O` | `Cmd + O` |
| 保存 | `Ctrl + S` | `Cmd + S` |
| すべて保存 | `Ctrl + K` → `S` | `Cmd + K` → `S` |
| ターミナル表示 | `` Ctrl + ` `` | `` Cmd + ` `` |
| コピー | `Ctrl + C` | `Cmd + C` |
| 貼り付け | `Ctrl + V` | `Cmd + V` |
| 切り取り | `Ctrl + X` | `Cmd + X` |
| 元に戻す | `Ctrl + Z` | `Cmd + Z` |
| 検索 | `Ctrl + F` | `Cmd + F` |
| 置換 | `Ctrl + H` | `Cmd + H` |

**基本的なパターン：**
- Windows: `Ctrl`
- Mac: `Cmd`（Command キー）

### ターミナル内

| 操作 | Windows | Mac |
|------|---------|-----|
| プロセス中断 | `Ctrl + C` | `Ctrl + C` |
| コピー（選択後） | `Ctrl + C` または 右クリック | `Cmd + C` |
| 貼り付け | `Ctrl + V` または 右クリック | `Cmd + V` |

---

## パスの記法の違い

### パスの区切り文字

| OS | 区切り文字 | 例 |
|----|-----------|---|
| Windows | `\` (バックスラッシュ) | `C:\Users\username\Documents` |
| Mac/Linux | `/` (スラッシュ) | `/Users/username/Documents` |

### Pythonでのパス指定

**Windows：**
```python
# 方法1：スラッシュを使う（推奨）
path = "C:/Users/username/Documents/data.csv"

# 方法2：rawストリング
path = r"C:\Users\username\Documents\data.csv"

# 方法3：バックスラッシュを2つ
path = "C:\\Users\\username\\Documents\\data.csv"
```

**Mac：**
```python
# スラッシュのみ
path = "/Users/username/Documents/data.csv"
```

### ホームディレクトリ

| OS | パス | 展開後の例 |
|----|------|-----------|
| Windows | `%USERPROFILE%` | `C:\Users\username` |
| Mac/Linux | `~` | `/Users/username` |

**Pythonでの取得：**
```python
import os

# どちらのOSでも動作
home = os.path.expanduser("~")
print(home)

# Windows: C:\Users\username
# Mac: /Users/username
```

### 絶対パスと相対パス

両方のOSで共通のルールですが、記法が異なります。

```python
# 相対パス（どちらも同じ）
"data/sales.csv"
"../output/result.txt"

# 絶対パス（OSで異なる）
# Windows
"C:/Users/username/project/data.csv"

# Mac
"/Users/username/project/data.csv"
```

---

## ターミナル・シェルの違い

### Windows

**種類：**
- **コマンドプロンプト (cmd.exe)** - 標準
- **PowerShell** - 高機能版
- **Anaconda Prompt** - conda専用（推奨）

**起動方法：**
1. スタートメニュー
2. 「Anaconda Prompt」と入力
3. 「Anaconda Prompt (miniconda3)」を選択

**プロンプト表示：**
```
(base) C:\Users\username>
```

### Mac/Linux

**種類：**
- **bash** - 古い標準
- **zsh** - 新しい標準（macOS Catalina以降）

**起動方法：**
1. Spotlight検索（`Cmd + Space`）
2. 「ターミナル」と入力
3. Enter

**プロンプト表示：**
```
(base) username@MacBook-Pro ~ %
```

### 初期化コマンド

| OS | コマンド |
|----|---------|
| Windows (cmd) | `conda init cmd.exe` |
| Windows (PowerShell) | `conda init powershell` |
| Mac (zsh) | `conda init zsh` |
| Mac (bash) | `conda init bash` |

---

## インストール手順の違い

### Miniconda

**Windows：**
1. `.exe` ファイルをダウンロード
2. インストーラーを実行
3. インストール時のオプション：
   - 「Just Me」を選択
   - 「Add to PATH」は**チェックしない**
   - 「Register as default Python」にチェック

**Mac：**
1. `.pkg` ファイルをダウンロード（Intel/Apple Silicon用を選択）
2. インストーラーを実行
3. インストール後、ターミナルで：
   ```bash
   conda init zsh
   ```
4. ターミナルを再起動

### VS Code

**Windows：**
1. `.exe` ファイルをダウンロード
2. インストーラーを実行
3. オプションで以下にチェック：
   - デスクトップアイコン作成
   - PATHに追加
   - コンテキストメニューに追加

**Mac：**
1. `.zip` ファイルをダウンロード
2. 解凍して `Visual Studio Code.app` を「アプリケーション」フォルダにドラッグ
3. 「アプリケーション」から起動

---

## よくある環境固有の問題

### Windows固有の問題

#### 問題1：「Windows Defender SmartScreen」の警告

**症状：** Minicondaインストール時に警告が出る

**解決方法：**
1. 「詳細情報」をクリック
2. 「実行」をクリック
3. 公式サイトからダウンロードした場合は安全です

#### 問題2：日本語の文字化け

**症状：** コマンドプロンプトで日本語が文字化けする

**解決方法：**
```bash
# UTF-8に変更
chcp 65001
```

または、VS Codeのターミナルを使う（推奨）

#### 問題3：「python」と入力するとMicrosoft Storeが開く

**症状：** `python` コマンドでMicrosoft Storeが起動する

**解決方法：**
1. 「設定」→「アプリ」→「アプリと機能」
2. 「アプリ実行エイリアス」をクリック
3. 「アプリインストーラー python.exe」をオフにする

または、Anaconda Promptを使う（推奨）

#### 問題4：ファイルパスにスペースや日本語

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

### Mac固有の問題

#### 問題1：「"Miniconda3"は開発元が未確認のため開けません」

**症状：** インストーラーが起動できない

**解決方法：**
1. システム環境設定 → セキュリティとプライバシー
2. 「このまま開く」をクリック

#### 問題2：conda コマンドが認識されない

**症状：** `zsh: command not found: conda`

**解決方法：**
```bash
# 初期化
~/miniconda3/bin/conda init zsh

# ターミナルを再起動
```

#### 問題3：Python 2 がデフォルトで起動する

**症状：** `python --version` で `Python 2.7.x` と表示される

**解決方法：**
```bash
# python3 を使う
python3 --version

# または、conda環境をアクティベート
conda activate myproject
python --version  # conda環境のPythonが使われる
```

#### 問題4：「xcrun: error」が出る

**症状：** gitなどのコマンド使用時にエラー

**解決方法：**
```bash
# Xcode Command Line Toolsをインストール
xcode-select --install
```

---

## クロスプラットフォーム対応のヒント

チーム内にWindows/Mac混在がある場合の対応方法。

### パス処理

```python
import os

# OSに依存しないパス結合
path = os.path.join("data", "sales.csv")
# Windows: data\sales.csv
# Mac: data/sales.csv

# ホームディレクトリ
home = os.path.expanduser("~")

# カレントディレクトリ
current = os.getcwd()
```

### 環境情報の取得

```python
import platform

# OS名
os_name = platform.system()
# 'Windows', 'Darwin'(Mac), 'Linux'

# 条件分岐
if os_name == "Windows":
    print("Windowsです")
elif os_name == "Darwin":
    print("Macです")
```

### 改行コードの違い

| OS | 改行コード |
|----|-----------|
| Windows | `\r\n` (CRLF) |
| Mac/Linux | `\n` (LF) |

**Pythonでの対処：**
```python
# Pythonが自動で変換してくれるので、通常は気にしなくてOK
with open("file.txt", "r") as f:
    content = f.read()
```

**VS Codeでの確認：**
- 右下のステータスバーに「CRLF」または「LF」と表示される
- クリックして変更可能

---

## environment.ymlでの環境共有

Windows/Mac間で環境を共有する場合。

### Windows で作成

```bash
# Windows
conda env export > environment.yml
```

### Mac でインポート

```bash
# Mac
conda env create -f environment.yml
```

**注意点：**
- 一部のパッケージはOS固有の場合がある
- その場合はエラーメッセージを確認して個別対応

### OSに依存しない environment.yml

```bash
# OSに依存しないパッケージのみをエクスポート
conda env export --from-history > environment.yml
```

これで、明示的にインストールしたパッケージのみが記録されます。

---

## まとめ

### 主な違い一覧

| 項目 | Windows | Mac |
|------|---------|-----|
| ターミナル | Anaconda Prompt | ターミナル.app |
| シェル | cmd / PowerShell | zsh / bash |
| パス区切り | `\` | `/` |
| ファイル一覧 | `dir` | `ls` |
| テキスト検索 | `findstr` | `grep` |
| ショートカット | `Ctrl` | `Cmd` |
| 改行コード | CRLF | LF |

### 共通で使えるもの

以下は OS に依存しません：

- conda コマンド（`conda install`, `conda create` など）
- Python コード（パスの書き方に注意）
- VS Code（ショートカットが違うだけ）
- pandas, numpy などのライブラリ

### 推奨事項

**Windows ユーザー：**
- Anaconda Prompt を使う
- パスは `/` を使う習慣をつける
- VS Code のターミナルを活用

**Mac ユーザー：**
- `conda init zsh` を忘れずに
- `python3` コマンドを使う場合は環境をアクティベート

**チーム開発：**
- `environment.yml` で環境を共有
- パスは `os.path` を使う
- 改行コードは LF に統一（推奨）

---

**目次に戻る：** [第0章：目次](./第0章_目次.md)
