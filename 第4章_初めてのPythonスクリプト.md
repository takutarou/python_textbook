# 第4章：初めてのPythonスクリプト

## この章で学ぶこと
- VS Codeでプロジェクトを開く正しい手順
- 初めてのPythonスクリプトを作成して実行する
- よくあるエラーとその対処法
- スクリプトの基本構造

いよいよ実際にPythonコードを書いて実行します！

---

## 4.1 VS Codeでプロジェクトを開く

### フォルダを開く操作

Pythonプロジェクトを始める時は、必ず**フォルダ単位で開く**ことが重要です。

#### ステップ1：VS Codeを起動

- デスクトップのアイコンから起動
- またはスタートメニュー（Windows）/アプリケーション（Mac）から起動

#### ステップ2：フォルダを開く

**方法1：メニューから**
1. 「ファイル」→「フォルダーを開く」（Macは「フォルダを開く」）
2. プロジェクトフォルダを選択（例：`data_analysis_project`）
3. 「フォルダーの選択」をクリック

**方法2：ドラッグ&ドロップ**
- エクスプローラー/Finderからフォルダを、VS Codeのウィンドウにドラッグ

**方法3：最近開いたフォルダから**
- 「ファイル」→「最近使用した項目を開く」
- 以前開いたフォルダの一覧から選択

#### ステップ3：フォルダが開いたことを確認

左側のエクスプローラーに、フォルダ名が大文字で表示されます：

```
EXPLORER
├─ DATA_ANALYSIS_PROJECT
    └─ (まだファイルはない)
```

### ターミナルの表示方法

VS Code内でコマンドを実行するには、ターミナルを開きます。

**開き方：**

方法1：**ショートカットキー**
- Windows: `` Ctrl + ` ``（バッククォート）
- Mac: `` Cmd + ` ``（バッククォート）

方法2：**メニューから**
- 「表示」→「ターミナル」

方法3：**上部メニューから**
- 「ターミナル」→「新しいターミナル」

**ターミナルが表示される場所：**
- VS Codeウィンドウの下部にパネルが開く
- ここでコマンドを実行できる

### Python環境（インタープリタ）の選択

スクリプトを実行する前に、正しいPython環境を選択することが**非常に重要**です。

#### 現在の環境を確認

VS Code右下のステータスバーを見てください：

```
Python 3.11.5 ('base': conda)
```

または

```
Python 3.11.5 ('data_analysis': conda)
```

#### 環境の選択手順

**ステップ1：選択画面を開く**

方法1：
- 右下のPythonバージョン表示をクリック

方法2：
- `Ctrl + Shift + P`（Mac: `Cmd + Shift + P`）
- `Python: Select Interpreter` と入力してEnter

**ステップ2：環境を選ぶ**

表示される一覧から、使いたい環境を選択：

```
> Python 3.11.5 ('data_analysis': conda)    ← プロジェクト用環境を選択
  Python 3.11.5 ('base': conda)
  Python 3.10.0 64-bit
```

**ステップ3：ターミナルを再起動**

- 既存のターミナルは古い環境のまま
- ターミナルの右上のゴミ箱アイコンをクリックして閉じる
- 新しくターミナルを開く（`` Ctrl + ` ``）

**ステップ4：確認**

ターミナルのプロンプトを確認：

```
(data_analysis) C:\Users\username\Documents\python_projects\data_analysis_project>
```

`(data_analysis)` と表示されていればOK！

---

## 4.2 Hello Worldを実行する

プログラミング学習の最初は「Hello World」が伝統です。画面に文字を表示する簡単なプログラムを作りましょう。

### .pyファイルの作成

#### ステップ1：新しいファイルを作成

**方法1：エクスプローラーから**
1. 左側のエクスプローラーで、フォルダ名の右にある「新しいファイル」アイコンをクリック
2. ファイル名を入力：`hello.py`
3. Enterを押す

**方法2：メニューから**
1. 「ファイル」→「新規ファイル」
2. 言語の選択で「Python」を選ぶ
3. `Ctrl + S`（Mac: `Cmd + S`）で保存
4. ファイル名を `hello.py` にして保存

**重要：**
- ファイルの拡張子は必ず `.py` にする
- これがPythonファイルの印
- ファイル名に日本語やスペースは使わない

#### ステップ2：コードを書く

エディタに以下のコードを入力してください：

```python
print("Hello World")
```

**コードの説明：**
- `print()`：画面に文字を表示する関数
- `"Hello World"`：表示したい文字列（ダブルクォートで囲む）
- 文字列はシングルクォート `'Hello World'` でもOK

#### ステップ3：ファイルを保存

- `Ctrl + S`（Mac: `Cmd + S`）で保存
- ファイル名の横の「●」が消えれば保存完了

### print文の書き方

#### 基本形

```python
print("表示したい内容")
```

#### 複数の内容を表示

```python
print("Hello", "World")
```

出力：
```
Hello World
```

#### 数値を表示

```python
print(100)
print(3.14)
```

出力：
```
100
3.14
```

#### 計算結果を表示

```python
print(10 + 5)
print(100 * 2)
```

出力：
```
15
200
```

#### 複数行のprint文

```python
print("1行目")
print("2行目")
print("3行目")
```

出力：
```
1行目
2行目
3行目
```

### 実行方法

Pythonスクリプトを実行する方法は複数あります。

#### 方法1：VS Codeの実行ボタン（初心者向け）

1. エディタの右上にある「▶」（再生ボタン）をクリック
2. ターミナルに結果が表示される

**出力例：**
```
(data_analysis) PS C:\Users\username\Documents\python_projects\data_analysis_project> python hello.py
Hello World
```

#### 方法2：ターミナルから実行（推奨）

ターミナルで以下のコマンドを入力：

```bash
python hello.py
```

Enterを押すと実行されます。

**出力：**
```
Hello World
```

#### 方法3：右クリックメニューから

1. エディタ内で右クリック
2. 「Run Python File in Terminal」を選択

**どの方法を使っても同じ結果になります！**

### 実行の仕組み

```
hello.py（あなたが書いたコード）
    ↓
python hello.py（実行コマンド）
    ↓
Pythonインタープリタが読み込む
    ↓
コードを1行ずつ実行
    ↓
print文の内容を画面に出力
    ↓
"Hello World" が表示される
```

---

## 4.3 よくあるエラーと対処法

初心者が最も頻繁に遭遇するエラーとその解決方法を紹介します。

### エラー1：「conda: command not found」（Mac）

**エラーメッセージ：**
```
zsh: command not found: conda
```

**原因：**
- condaがターミナルに認識されていない
- Minicondaのインストール時にターミナル初期化をしていない

**対処法：**
```bash
# ホームディレクトリに移動
cd ~

# conda初期化
~/miniconda3/bin/conda init zsh

# ターミナルを再起動
```

ターミナルを閉じて再度開けば、`(base)` と表示されるはずです。

### エラー2：「'python' は、内部コマンドまたは外部コマンド...」（Windows）

**エラーメッセージ：**
```
'python' は、内部コマンドまたは外部コマンド、
操作可能なプログラムまたはバッチ ファイルとして認識されていません。
```

**原因1：Anaconda Promptではなく、通常のコマンドプロンプトを使っている**

**対処法：**
- VS Codeを閉じる
- スタートメニューから「Anaconda Prompt (miniconda3)」を起動
- そこから `code .` コマンドでVS Codeを開く

**原因2：VS Codeのターミナルがconda未対応**

**対処法：**
```bash
# VS Codeのターミナルで実行
conda init cmd.exe

# VS Codeを再起動
```

### エラー3：環境がアクティベートされていない

**症状：**
- ターミナルのプロンプトが `(base)` のまま
- 本来は `(data_analysis)` など、プロジェクト環境になるべき

**原因：**
- VS Codeで環境を選択していない
- または、ターミナルを再起動していない

**対処法：**
1. VS Code右下のPythonバージョン表示をクリック
2. 正しい環境（例：`data_analysis`）を選択
3. ターミナルを閉じて新しく開く
4. プロンプトが `(data_analysis)` になることを確認

### エラー4：IndentationError（インデントエラー）

**エラーメッセージ：**
```python
  File "hello.py", line 2
    print("Hello")
    ^
IndentationError: unexpected indent
```

**原因：**
不要な空白やタブが入っている

**間違った例：**
```python
    print("Hello World")  ← 行頭にスペースが入っている
```

**正しい例：**
```python
print("Hello World")  ← 行頭から書き始める
```

**対処法：**
- 行頭の余計な空白を削除
- Pythonではインデント（字下げ）が重要な意味を持つため、不要な空白は厳禁

### エラー5：SyntaxError: invalid syntax（文法エラー）

**エラーメッセージ：**
```python
  File "hello.py", line 1
    print("Hello World"
                       ^
SyntaxError: invalid syntax
```

**原因：**
括弧やクォートの閉じ忘れ

**間違った例：**
```python
print("Hello World"  ← 閉じ括弧がない
print('Hello World"  ← クォートの種類が違う
```

**正しい例：**
```python
print("Hello World")  ← 括弧を閉じる
print('Hello World')  ← クォートは統一
```

**対処法：**
- エラーメッセージの `^` マークの位置を確認
- 括弧 `()` やクォート `""` が対になっているか確認

### エラー6：FileNotFoundError（ファイルが見つからない）

**エラーメッセージ：**
```
python: can't open file 'hello.py': [Errno 2] No such file or directory
```

**原因：**
- ターミナルのカレントディレクトリが間違っている
- ファイル名が間違っている

**対処法：**

1. 現在のディレクトリを確認：
   ```bash
   # Windows
   cd

   # Mac
   pwd
   ```

2. 正しいディレクトリに移動：
   ```bash
   # Windows
   cd C:\Users\username\Documents\python_projects\data_analysis_project

   # Mac
   cd ~/Documents/python_projects/data_analysis_project
   ```

3. ファイルが存在するか確認：
   ```bash
   # Windows
   dir

   # Mac
   ls
   ```

4. VS Codeでフォルダを開いている場合、ターミナルは自動的にそのフォルダで開くので、通常この問題は起きません

### エラー7：日本語の文字化け（Windows）

**症状：**
```python
print("こんにちは")
```

実行すると：
```
縺薙ｓ縺ｫ縺｡縺ｯ
```

**原因：**
ファイルの文字コードが正しくない

**対処法：**

1. VS Code右下の文字コード表示（例：`SJIS`）をクリック
2. 「エンコード付きで保存」を選択
3. `UTF-8` を選択
4. ファイルを保存し直す
5. 再度実行

**予防策：**
- VS Codeの設定で、デフォルトを UTF-8 にしておく
- 設定 → `files.encoding` を検索 → `utf8` に設定

---

## 4.4 スクリプトの基本構造

### コメントの書き方

コードに説明を書くための「コメント」という機能があります。

#### 1行コメント

```python
# これはコメントです。実行されません。
print("Hello World")  # 行の途中からコメントも可能

# print("このprintは実行されません")
```

**ポイント：**
- `#` 以降、その行の最後までがコメント
- Pythonは無視して実行しない
- コードの説明や、一時的にコードを無効化するのに使う

#### 複数行コメント

```python
"""
これは複数行のコメントです。
何行でも書けます。
通常はファイルの先頭に、スクリプトの説明を書きます。
"""

print("Hello World")
```

または

```python
'''
シングルクォート3つでも
複数行コメントになります。
'''

print("Hello World")
```

**用途：**
- ファイルの先頭に、スクリプトの目的を説明
- 関数の説明（後の章で学びます）

#### コメントの良い例

```python
# データ分析スクリプト
# 作成日：2024-01-15
# 目的：売上データを集計する

# ライブラリの読み込み
import pandas as pd

# データの読み込み
data = pd.read_csv("sales.csv")

# データの集計
total = data["amount"].sum()  # 合計金額を計算

print(f"合計: {total}円")
```

### 変数と基本的な演算

#### 変数とは

値を入れておく「箱」のようなもの。

```python
# 変数に値を代入
name = "太郎"
age = 25
height = 170.5

# 変数を使って表示
print(name)      # 太郎
print(age)       # 25
print(height)    # 170.5
```

#### 変数名のルール

**✅ 良い変数名：**
```python
name = "太郎"
user_age = 25
total_price = 1000
data_2024 = [1, 2, 3]
```

**❌ 使えない/避けるべき変数名：**
```python
# エラーになるもの
2024_data = [1, 2, 3]  # 数字から始まる
user-age = 25          # ハイフンは使えない
my name = "太郎"       # スペースは使えない

# 避けるべきもの
a = 100                # 何の値か分からない
x = "user123"          # 内容が不明
print = "test"         # 組み込み関数名は使わない
```

**命名のベストプラクティス：**
- 小文字とアンダースコアを使う（`user_name`）
- 内容が分かる名前にする
- 短すぎず、長すぎず

#### 基本的な演算

```python
# 四則演算
a = 10
b = 3

print(a + b)   # 13（足し算）
print(a - b)   # 7（引き算）
print(a * b)   # 30（掛け算）
print(a / b)   # 3.333...（割り算）
print(a // b)  # 3（割り算の商）
print(a % b)   # 1（割り算の余り）
print(a ** b)  # 1000（べき乗：10の3乗）
```

```python
# 文字列の連結
first_name = "山田"
last_name = "太郎"
full_name = first_name + last_name
print(full_name)  # 山田太郎

# 文字列の繰り返し
print("Hello " * 3)  # Hello Hello Hello
```

```python
# 変数の更新
count = 0
print(count)    # 0

count = count + 1
print(count)    # 1

# 短縮形
count += 1      # count = count + 1 と同じ
print(count)    # 2
```

### print文での出力（応用）

#### f-string（フォーマット済み文字列）

変数を文字列に埋め込む便利な方法：

```python
name = "太郎"
age = 25

# 従来の方法
print("私の名前は" + name + "です。年齢は" + str(age) + "歳です。")

# f-stringを使う方法（推奨）
print(f"私の名前は{name}です。年齢は{age}歳です。")
```

出力：
```
私の名前は太郎です。年齢は25歳です。
```

**メリット：**
- 読みやすい
- 型変換（`str()`）が不要
- 計算結果も埋め込める

```python
price = 1000
quantity = 3

print(f"合計金額は{price * quantity}円です。")
# 合計金額は3000円です。
```

#### 改行や特殊文字

```python
# 改行：\n
print("1行目\n2行目\n3行目")

# タブ：\t
print("名前\t年齢\t職業")
print("太郎\t25\t会社員")
```

出力：
```
1行目
2行目
3行目

名前    年齢    職業
太郎    25      会社員
```

---

## 実践：簡単な計算スクリプトを作ってみよう

学んだ知識を使って、実用的なスクリプトを作ってみましょう。

### 課題：消費税計算プログラム

商品の価格から消費税込みの金額を計算するスクリプトを作ります。

**新しいファイルを作成：`tax_calculator.py`**

```python
# 消費税計算プログラム
# 作成日：2024-01-15

# 商品の価格（税抜）
price = 1000

# 消費税率
tax_rate = 0.1  # 10%

# 消費税額を計算
tax = price * tax_rate

# 税込価格を計算
total = price + tax

# 結果を表示
print("=== 消費税計算 ===")
print(f"商品価格: {price}円")
print(f"消費税額: {tax}円")
print(f"税込価格: {total}円")
```

**実行方法：**
```bash
python tax_calculator.py
```

**出力：**
```
=== 消費税計算 ===
商品価格: 1000円
消費税額: 100.0円
税込価格: 1100.0円
```

**応用：複数の商品**

```python
# 複数商品の税込計算

# 商品リスト（価格）
item1 = 1000
item2 = 2500
item3 = 800

# 小計
subtotal = item1 + item2 + item3

# 消費税
tax_rate = 0.1
tax = subtotal * tax_rate

# 合計
total = subtotal + tax

# 結果表示
print("=== お会計 ===")
print(f"商品1: {item1}円")
print(f"商品2: {item2}円")
print(f"商品3: {item3}円")
print(f"小計: {subtotal}円")
print(f"消費税: {tax}円")
print(f"合計: {total}円")
```

---

## まとめ

この章では、初めてのPythonスクリプトを作成・実行しました：

- ✅ VS Codeでプロジェクトフォルダを開く
- ✅ Python環境（インタープリタ）を選択
- ✅ `.py` ファイルを作成
- ✅ `print()` 文で画面に出力
- ✅ スクリプトを実行する複数の方法
- ✅ よくあるエラーとその対処法
- ✅ コメントの書き方
- ✅ 変数と基本的な演算
- ✅ f-stringを使った出力

**重要なポイント：**
1. 必ず環境をアクティベートしてから実行
2. エラーメッセージをよく読む
3. コメントを活用してコードを説明
4. 変数名は分かりやすく

次の章では、外部ライブラリの使い方を学びます。ここが初心者が最もつまずきやすいポイントです！

---

## 確認問題

1. Pythonファイルの拡張子は何ですか？
2. 画面に文字を表示する関数は何ですか？
3. `#` から始まる行は何と呼ばれますか？その役割は？
4. 変数名に使えない文字は何ですか？（3つ挙げてください）
5. f-stringを使って、変数 `name = "太郎"` を「私の名前は太郎です」と表示するコードを書いてください

---

**前の章へ：** [第3章：conda環境の理解と作成](./第3章_conda環境の理解と作成.md)
**次の章へ：** [第5章：ライブラリの理解](./第5章_ライブラリの理解.md)
