# 付録D：トラブルシューティングQ&A

よくある質問と解決方法をFAQ形式でまとめています。
困った時は、まずこのページで該当する質問を探してください。

---

## 目次

1. [環境構築編](#環境構築編)
2. [環境管理編](#環境管理編)
3. [ライブラリ編](#ライブラリ編)
4. [ファイル操作編](#ファイル操作編)
5. [エラー編](#エラー編)
6. [VS Code編](#vs-code編)
7. [その他](#その他)

---

## 環境構築編

### Q1: Minicondaをインストールしたが、conda コマンドが認識されない

**症状：**
```
'conda' は、内部コマンドまたは外部コマンド、
操作可能なプログラムまたはバッチ ファイルとして認識されていません。
```

**原因：** 通常のコマンドプロンプトを使っている

**解決方法：**
1. スタートメニューを開く
2. 「Anaconda Prompt」と入力して検索
3. 「Anaconda Prompt (miniconda3)」を起動
4. `conda --version` で確認

**関連：** [第2章 2.1](./第2章_環境構築.md#21-minicondaのインストール)

---

### Q2: VS Codeのターミナルでcondaコマンドが使えない

**症状：** VS Codeのターミナルで `conda` と入力してもエラーになる

**解決方法：**
```bash
# VS Codeのターミナルで実行
conda init cmd.exe

# VS Codeを完全に閉じて再起動
```

再起動後、ターミナルを開くと `(base)` と表示されるはず。

**関連：** [第2章 2.2](./第2章_環境構築.md#22-vs-codeのセットアップ)

---

### Q3: Pythonをインストールしたのに、python コマンドが使えない

**症状：** `python` と入力すると Microsoft Store が開く

**原因：** conda環境がアクティベートされていない、またはPythonがインストールされていない

**解決方法：**
```bash
# 環境を確認
conda env list

# 環境をアクティベート
conda activate 環境名

# Pythonバージョンを確認
python --version
```

**関連：** [第3章 3.3](./第3章_conda環境の理解と作成.md#33-conda環境のアクティベートデアクティベート)

---

## 環境管理編

### Q4: 環境をアクティベートしたのに、プロンプトが変わらない

**症状：** `conda activate myproject` を実行しても、プロンプトが `(base)` のまま

**原因：** 環境名が間違っているか、環境が存在しない

**解決方法：**
```bash
# 環境一覧を確認
conda env list

# 正しい環境名を確認して再実行
conda activate 正しい環境名
```

**関連：** [第7章 7.1](./第7章_つまずきポイント集.md#71-環境関連でよくある問題)

---

### Q5: base環境で作業してしまった。どうすればいい？

**症状：** プロジェクト用の環境を作ったが、base環境で作業してしまった

**解決方法：**
```bash
# 今すぐ正しい環境に切り替える
conda activate myproject

# base環境にインストールしたパッケージは削除（オプション）
conda activate base
conda uninstall パッケージ名

# プロジェクト環境に改めてインストール
conda activate myproject
conda install パッケージ名
```

**予防策：** 作業前に必ずプロンプトを確認する習慣をつける

**関連：** [第7章 7.1](./第7章_つまずきポイント集.md#問題1base環境で作業してしまう)

---

### Q6: VS Code右下の環境とターミナルの環境が違う

**症状：**
- VS Code右下：`Python 3.11.5 ('base': conda)`
- ターミナル：`(myproject) C:\Users\username>`

**解決方法：**
1. VS Code右下のPythonバージョン表示をクリック
2. `Python 3.11.5 ('myproject': conda)` を選択
3. 既存のターミナルを閉じる（ゴミ箱アイコン）
4. 新しくターミナルを開く（`` Ctrl + ` ``）
5. 両方が `myproject` になることを確認

**関連：** [第7章 7.1](./第7章_つまずきポイント集.md#問題3vs-codeのインタープリタ選択を間違える)

---

### Q7: 環境を削除したい

**解決方法：**
```bash
# 削除したい環境がアクティブな場合、まずデアクティベート
conda deactivate

# 環境を削除
conda env remove -n 削除したい環境名

# 確認
conda env list
```

**注意：** base環境は削除できません。

---

## ライブラリ編

### Q8: ModuleNotFoundError: No module named 'pandas'

**症状：**
```python
import pandas as pd
# ModuleNotFoundError: No module named 'pandas'
```

**原因チェックリスト：**

**1. ライブラリがインストールされていない**
```bash
# 確認
conda list | findstr pandas

# インストール
conda install pandas
```

**2. 違う環境にインストールしている**
```bash
# 現在の環境を確認
conda env list
# *がどの環境についているか確認

# 正しい環境をアクティベート
conda activate 正しい環境名

# その環境にインストール
conda install pandas
```

**3. VS Codeの環境設定が間違っている**
- VS Code右下の環境表示を確認
- プロジェクトの環境を選択し直す

**関連：** [第5章 5.2](./第5章_ライブラリの理解.md#52-インストールとインポートの決定的な違い), [第7章 7.4](./第7章_つまずきポイント集.md#エラー1moduleno founderror)

---

### Q9: インストールしたのに import でエラーが出る

**症状：**
```bash
# インストールは成功
(myproject) > conda install pandas
# Successfully installed

# でもimportでエラー
>>> import pandas
ModuleNotFoundError: No module named 'pandas'
```

**原因：** Pythonを起動している環境が違う

**解決方法：**
```bash
# 一度Pythonを終了
>>> exit()

# 環境を確認
conda env list

# 正しい環境をアクティベート
conda activate myproject

# 環境にパッケージがあるか確認
conda list | findstr pandas

# Pythonを再起動
python
>>> import pandas
# 成功するはず
```

**関連：** [第5章 5.2](./第5章_ライブラリの理解.md#パターン3別の環境にインストールしてしまった)

---

### Q10: conda install が遅い、または途中で止まる

**症状：** `conda install` を実行すると、パッケージのダウンロードが非常に遅い

**解決方法：**

**方法1：時間を置いて再試行**
```bash
# Ctrl+C で一度中断
# しばらく待ってから再実行
conda install パッケージ名
```

**方法2：チャンネルを変更**
```bash
# conda-forgeチャンネルから試す
conda install -c conda-forge パッケージ名
```

**方法3：キャッシュをクリア**
```bash
conda clean --all
conda install パッケージ名
```

---

## ファイル操作編

### Q11: FileNotFoundError: [Errno 2] No such file or directory

**症状：**
```python
data = pd.read_csv("sales.csv")
# FileNotFoundError: [Errno 2] No such file or directory: 'sales.csv'
```

**原因チェックリスト：**

**1. ファイルが存在しない**
```bash
# ファイル一覧を確認
dir

# ファイル名を確認（大文字・小文字も）
```

**2. カレントディレクトリが違う**
```bash
# 現在地を確認
cd

# プロジェクトフォルダに移動
cd C:\Users\username\Documents\python_projects\myproject
```

**3. ファイル名が違う**
- `Sales.csv` と `sales.csv` は別ファイル
- スペースが含まれていないか確認
- 拡張子が正しいか確認（`.csv.txt` になっていないか）

**解決方法：**
```python
# 絶対パスで指定してみる
data = pd.read_csv(r"C:\Users\username\Documents\python_projects\myproject\sales.csv")

# または、ファイルの存在を確認
import os
print(os.path.exists("sales.csv"))  # True なら存在する
```

**関連：** [第7章 7.2](./第7章_つまずきポイント集.md#72-パスの問題)

---

### Q12: CSVファイルを読み込むと文字化けする

**症状：**
```python
data = pd.read_csv("sales.csv")
print(data)
# 日本語が文字化けして表示される
```

**解決方法：**
```python
# Shift-JIS で読み込む
data = pd.read_csv("sales.csv", encoding="shift_jis")

# それでもダメなら cp932
data = pd.read_csv("sales.csv", encoding="cp932")

# または UTF-8
data = pd.read_csv("sales.csv", encoding="utf-8")
```

**予防策：**
Excelで保存する時、「CSV UTF-8（コンマ区切り）」を選択

**関連：** [第7章 7.3](./第7章_つまずきポイント集.md#問題2csvファイルを読み込むと文字化け)

---

### Q13: パスにバックスラッシュを使うとエラーになる

**症状：**
```python
data = pd.read_csv("C:\Users\username\data.csv")
# SyntaxError
```

**原因：** `\U` などがエスケープ文字として解釈される

**解決方法：**

**方法1：スラッシュを使う（推奨）**
```python
data = pd.read_csv("C:/Users/username/data.csv")
```

**方法2：rawストリング**
```python
data = pd.read_csv(r"C:\Users\username\data.csv")
```

**方法3：バックスラッシュを2つ**
```python
data = pd.read_csv("C:\\Users\\username\\data.csv")
```

**関連：** [第7章 7.2](./第7章_つまずきポイント集.md#問題3windowsのバックスラッシュ問題)

---

## エラー編

### Q14: SyntaxError: invalid syntax

**よくある原因：**

**原因1：括弧の閉じ忘れ**
```python
# 間違い
print("Hello"

# 正しい
print("Hello")
```

**原因2：コロンの忘れ**
```python
# 間違い
if x > 0
    print("positive")

# 正しい
if x > 0:
    print("positive")
```

**原因3：クォートの不一致**
```python
# 間違い
name = "太郎'

# 正しい
name = "太郎"
```

**関連：** [第7章 7.4](./第7章_つまずきポイント集.md#エラー2syntaxerror文法エラー)

---

### Q15: IndentationError: unexpected indent

**症状：**
```python
def calculate():
    x = 10
        y = 20  # IndentationError
    return x + y
```

**原因：** インデント（字下げ）が不適切

**解決方法：**
```python
def calculate():
    x = 10
    y = 20  # インデントを揃える
    return x + y
```

**VS Codeの設定確認：**
1. 設定を開く（`Ctrl + ,`）
2. 「Tab Size」で検索
3. `4` に設定されているか確認
4. 「Insert Spaces」がオンになっているか確認

**関連：** [第7章 7.4](./第7章_つまずきポイント集.md#エラー3indentationerrorインデントエラー)

---

### Q16: NameError: name 'pd' is not defined

**症状：**
```python
data = pd.read_csv("sales.csv")
# NameError: name 'pd' is not defined
```

**原因：** import 文を書いていない

**解決方法：**
```python
# ファイルの先頭に追加
import pandas as pd

# これで使えるようになる
data = pd.read_csv("sales.csv")
```

**関連：** [第5章 5.2](./第5章_ライブラリの理解.md#パターン1インストールしたのにエラーが出る)

---

### Q17: KeyError: 'amount'

**症状：**
```python
total = data["amount"].sum()
# KeyError: 'amount'
```

**原因：** 指定した列名が存在しない

**解決方法：**
```python
# 列名を確認
print(data.columns)
# Index(['date', 'product', 'price'], dtype='object')

# 'amount' ではなく 'price' が正しい
total = data["price"].sum()
```

**よくある間違い：**
- タイプミス：`amount` vs `Amount`（大文字・小文字）
- スペース：`amount` vs `amount `（後ろにスペース）

**関連：** [第7章 7.4](./第7章_つまずきポイント集.md#エラー5keyerror辞書dataframeのキーエラー)

---

## VS Code編

### Q18: ショートカットキーが効かない

**症状：** `` Ctrl + ` `` でターミナルが開かない

**原因1：日本語入力モードになっている**
- 解決：`半角/全角` キーで英数モードに切り替え

**原因2：他のアプリと競合**
- 解決：メニューから「表示」→「ターミナル」で開く

**原因3：キーボードの違い**
- `` ` `` の位置がキーボードによって異なる

**関連：** [付録B](./付録B_VSCodeショートカット.md)

---

### Q19: VS Codeで作成したファイルが保存されない

**症状：** ファイルを作成して `Ctrl + S` を押したが、保存場所がわからない

**解決方法：**
1. VS Codeでフォルダを開き直す
2. 「ファイル」→「フォルダーを開く」
3. プロジェクトフォルダを選択
4. エクスプローラーで「新しいファイル」をクリック
5. ファイル名を入力
6. コードを書いて保存

**重要：** フォルダ単位で開く習慣をつける

**関連：** [第4章 4.1](./第4章_初めてのPythonスクリプト.md#41-vs-codeでプロジェクトを開く)

---

### Q20: VS Codeが日本語化されない

**解決方法：**
1. `Ctrl + Shift + X` で拡張機能を開く
2. 「Japanese Language Pack」で検索
3. インストール
4. VS Codeを再起動
5. 右下に表示される通知で「Change Language and Restart」をクリック

---

## その他

### Q21: Python 2 と Python 3 の違いは？

**回答：** この教材では Python 3 を使います。

- Python 2：2020年にサポート終了（古い）
- Python 3：現在の標準（これを使う）

conda環境を作成する時に `python=3.11` と指定すれば Python 3 がインストールされます。

---

### Q22: condaとpipの違いは？

**回答：** 両方ともパッケージ管理ツールですが、この教材では **conda** を使います。

| 項目 | conda | pip |
|------|-------|-----|
| インストール対象 | Python以外も | Pythonのみ |
| 環境管理 | できる | できない（venv併用） |
| 当社での推奨 | ✓ conda | - |

**理由：** conda の方が環境管理が簡単で、初心者向きです。

---

### Q23: Jupyter NotebookとPythonスクリプトの違いは？

**回答：**

- **Pythonスクリプト（.py）**：この教材で使用
  - テキストファイル
  - エディタで編集
  - `python script.py` で実行

- **Jupyter Notebook（.ipynb）**：発展編
  - ブラウザで操作
  - セル単位で実行
  - データ分析の対話的な作業に便利

**初心者は .py から始めることを推奨します。**

---

### Q24: エラーが解決しない。どうすればいい？

**手順：**

1. **このQ&Aを確認**
   - 似た問題がないか探す

2. **第7章を確認**
   - [つまずきポイント集](./第7章_つまずきポイント集.md)

3. **Google検索**
   - エラーメッセージをそのまま検索
   - 「python pandas エラーメッセージ」

4. **社内で質問**
   - [第8章 8.3](./第8章_情報収集とヘルプ.md#83-社内で質問する際のポイント) の質問テンプレートを使う
   - 環境情報、コード、エラーメッセージを共有

---

### Q25: もっと詳しく学ぶには？

**次のステップ：**

1. **公式ドキュメント**
   - [Python公式（日本語）](https://docs.python.org/ja/3/)
   - [pandas公式](https://pandas.pydata.org/docs/)

2. **オンライン学習**
   - Qiita、Zennで記事を読む
   - Stack Overflowで質問・回答を見る

3. **実践**
   - 実際の業務で使ってみる
   - 小さなプロジェクトから始める

**関連：** [第8章](./第8章_情報収集とヘルプ.md)

---

## クイックリファレンス

### エラー別の対処法早見表

| エラー | まず確認すること | 参照 |
|-------|---------------|------|
| ModuleNotFoundError | 環境、ライブラリインストール | [Q8](#q8-modulenotfounderror-no-module-named-pandas) |
| FileNotFoundError | ファイル名、カレントディレクトリ | [Q11](#q11-filenotfounderror-errno-2-no-such-file-or-directory) |
| SyntaxError | 括弧、コロン、クォート | [Q14](#q14-syntaxerror-invalid-syntax) |
| IndentationError | インデントの揃え | [Q15](#q15-indentationerror-unexpected-indent) |
| NameError | import文 | [Q16](#q16-nameerror-name-pd-is-not-defined) |
| KeyError | 列名、キー名 | [Q17](#q17-keyerror-amount) |

---

## まとめ

**困った時の3ステップ：**

1. **このQ&Aで検索**
   - `Ctrl + F` でページ内検索

2. **関連する章を読む**
   - 各Q&Aに関連章へのリンクあり

3. **それでも解決しない**
   - 社内で質問（[第8章 8.3](./第8章_情報収集とヘルプ.md#83-社内で質問する際のポイント)）

**最もよくある問題トップ3：**
1. 環境がアクティベートされていない → プロンプト確認
2. ライブラリがインストールされていない → `conda list`
3. import文を書いていない → スクリプトの先頭に追加

---

**目次に戻る：** [第0章：目次](./第0章_目次.md)
