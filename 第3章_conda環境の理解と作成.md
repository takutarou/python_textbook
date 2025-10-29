# 第3章：conda環境の理解と作成

## この章で学ぶこと
- conda環境の概念をより深く理解する
- 実際にプロジェクト用の環境を作成する
- 環境のアクティベート・デアクティベートの方法
- VS Codeで作成した環境を使う方法

この章では、Pythonプログラミングで最も重要な「環境管理」について、実践的に学びます。

---

## 3.1 conda環境とは何か（復習と深掘り）

### base環境と個別環境の違い

第1章で軽く触れましたが、ここで改めて詳しく説明します。

**base環境とは：**
- Minicondaをインストールした時に自動的に作られる「基本の環境」
- conda自体を動かすための環境
- ターミナルを開くと `(base)` と表示される

**個別環境とは：**
- プロジェクトごとに作成する「専用の環境」
- 自分で名前をつけて作成する
- 例：`(data_analysis)`, `(web_scraping)` など

### 環境の仕組みを図で理解する

```
あなたのPC
│
├─ (base) ← Minicondaの基本環境
│   ├─ Python 3.11
│   ├─ conda本体
│   └─ 最小限のパッケージ
│
├─ (project_a) ← プロジェクトA専用環境
│   ├─ Python 3.10
│   ├─ pandas 1.5.0
│   ├─ numpy 1.23.0
│   └─ matplotlib 3.6.0
│
└─ (project_b) ← プロジェクトB専用環境
    ├─ Python 3.11
    ├─ pandas 2.0.0
    ├─ numpy 1.24.0
    └─ scikit-learn 1.3.0
```

各環境は完全に独立していて、互いに影響を与えません。

### なぜプロジェクトごとに環境を分けるのか

#### 理由1：ライブラリのバージョン競合を防ぐ

**問題のシナリオ：**

あなたが2つのプロジェクトに取り組んでいるとします。

- **プロジェクトA**：去年作ったデータ分析スクリプト（pandas 1.5で動作）
- **プロジェクトB**：新しく作る機械学習プロジェクト（pandas 2.0が必要）

もし1つの環境で両方を管理すると：

```
同じ環境内
├─ pandas 1.5をインストール → プロジェクトAが動く
├─ pandas 2.0をインストール → 1.5が上書きされる
└─ プロジェクトAが動かなくなる！
```

環境を分ければ：

```
(project_a環境)
└─ pandas 1.5 → プロジェクトAはこちらで動かす

(project_b環境)
└─ pandas 2.0 → プロジェクトBはこちらで動かす
```

両方とも問題なく動きます！

#### 理由2：クリーンな状態を保てる

実験的にいろいろなライブラリを試したい時、専用の環境を作れば：
- 本番のプロジェクトに影響しない
- 失敗しても、その環境だけ削除すればOK
- いつでもクリーンな状態から再スタートできる

#### 理由3：他の人と環境を共有しやすい

環境の内容（どのライブラリのどのバージョンを使っているか）を記録しておけば：
- チームメンバーが同じ環境を再現できる
- 「私のPCでは動くのに...」という問題が減る

### 環境を分けないとどんな問題が起きるか

**よくある失敗例：**

```
全部base環境にインストールしてしまう
↓
ライブラリがどんどん増える
↓
バージョン競合が発生
↓
一部のライブラリが動かなくなる
↓
原因の特定が困難
↓
最悪の場合、conda自体が壊れる
```

**教訓：**
- **base環境には何もインストールしない**
- **プロジェクトごとに必ず新しい環境を作る**

---

## 3.2 conda環境の作成手順

### 基本的なコマンド

conda環境を作成する基本のコマンドは以下です：

```bash
conda create -n 環境名 python=バージョン
```

**パラメータの説明：**
- `-n`：name（名前）の略。環境名を指定する
- `環境名`：自分でつける環境の名前
- `python=バージョン`：使用するPythonのバージョン

### Pythonバージョンの指定方法

#### 推奨されるバージョン指定

```bash
# Python 3.11系の最新版を使う（推奨）
conda create -n myproject python=3.11

# Python 3.10系の最新版を使う
conda create -n myproject python=3.10

# Python 3.9系の最新版を使う
conda create -n myproject python=3.9
```

**ポイント：**
- マイナーバージョン（3.11, 3.10など）まで指定するのが一般的
- パッチバージョン（3.11.5など）は自動で最新が入る
- **特別な理由がない限り、Python 3.10以上を使いましょう**

#### バージョンを指定しない場合

```bash
# Pythonバージョンを指定しない（非推奨）
conda create -n myproject
```

この場合、Pythonがインストールされないので、後で手動でインストールする必要があります。
**必ずPythonバージョンを指定することを推奨します。**

### 環境名の付け方のルール

#### ✅ 良い環境名の例

```bash
# プロジェクト名をそのまま使う
conda create -n sales_analysis python=3.11

# 用途を明確に
conda create -n web_scraping python=3.11

# 日付を含める（複数バージョン管理する場合）
conda create -n project_2024 python=3.11
```

#### ❌ 避けるべき環境名

```bash
# 日本語（エラーの原因）
conda create -n データ分析 python=3.11

# スペース（エラーの原因）
conda create -n my project python=3.11

# 短すぎて内容がわからない
conda create -n p1 python=3.11

# 特殊文字
conda create -n project@2024 python=3.11
```

**命名規則：**
- 英数字とアンダースコア、ハイフンのみ
- 小文字推奨
- 内容が分かりやすい名前
- あまり長すぎない（20文字程度まで）

### 環境作成の実行例

実際にコマンドを実行してみましょう：

```bash
conda create -n first_project python=3.11
```

実行すると、以下のような出力が表示されます：

```
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /Users/username/miniconda3/envs/first_project

  added / updated specs:
    - python=3.11


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    python-3.11.5              |       h1234567_0         28.5 MB
    ...

The following NEW packages will be INSTALLED:

  python             pkgs/main/osx-64::python-3.11.5-h1234567_0
  ...

Proceed ([y]/n)?
```

**ここで `y` を入力してEnterを押します。**

```
Downloading and Extracting Packages
python-3.11.5        | 28.5 MB   | ##################################### | 100%
...

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate first_project
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

これで環境の作成が完了です！

### 環境の確認

作成した環境の一覧を確認するには：

```bash
conda env list
```

または

```bash
conda info --envs
```

出力例：

```
# conda environments:
#
base                  *  /Users/username/miniconda3
first_project            /Users/username/miniconda3/envs/first_project
```

**読み方：**
- `*`（アスタリスク）がついているのが現在アクティブな環境
- 各環境の保存場所（パス）も表示される

---

## 3.3 conda環境のアクティベート・デアクティベート

### アクティベート（環境を有効にする）

作成した環境を使うには、「アクティベート」する必要があります。

```bash
conda activate 環境名
```

**実行例：**

```bash
conda activate first_project
```

成功すると、プロンプトの表示が変わります：

```
# アクティベート前
(base) C:\Users\username>

# アクティベート後
(first_project) C:\Users\username>
```

```
# アクティベート前（Mac）
(base) username@MacBook-Pro ~ %

# アクティベート後
(first_project) username@MacBook-Pro ~ %
```

**これで `first_project` 環境が有効になりました！**

この状態で：
- Pythonを実行すると、この環境のPythonが使われる
- ライブラリをインストールすると、この環境にだけインストールされる

### デアクティベート（環境を無効にする）

作業が終わったら、環境を無効にします：

```bash
conda deactivate
```

プロンプトが `(base)` に戻ります：

```
# デアクティベート前
(first_project) C:\Users\username>

# デアクティベート後
(base) C:\Users\username>
```

### 重要な注意点

1. **base環境には戻るが、「環境なし」にはならない**
   - `conda deactivate` を実行すると base環境に戻る
   - 完全に環境から出るわけではない

2. **環境をアクティベートし忘れるのが最も多いミス**
   - ライブラリをインストールする前に、必ず環境をアクティベート
   - プロンプトの `()` 内を常に確認する習慣をつける

3. **ターミナルを閉じると、アクティベート状態はリセットされる**
   - 新しいターミナルを開いたら、また `conda activate` が必要

### VS Codeでの環境選択

VS Codeでは、ターミナルとは別に「どのPython環境を使うか」を選択できます。

#### ステップ1：インタープリタの選択画面を開く

方法1：**コマンドパレットから**
1. `Ctrl + Shift + P` を押す
2. `Python: Select Interpreter` と入力して選択

方法2：**ステータスバーから**
1. VS Code右下のステータスバーを確認
2. `Python 3.x.x ('base': conda)` のような表示をクリック

#### ステップ2：環境を選択

一覧から作成した環境を選びます：

```
Python 3.11.5 ('first_project': conda)    ← これを選択
Python 3.11.5 ('base': conda)
Python 3.10.0 64-bit
```

#### ステップ3：確認

- 右下のステータスバーが `Python 3.11.5 ('first_project': conda)` に変わる
- 新しいターミナルを開くと、自動的に `(first_project)` がアクティベートされる

**重要：**
- VS Codeでインタープリタを選択すると、新しいターミナルで自動アクティベートされる
- 既存のターミナルは変わらないので、一度閉じて新しく開く

---

## 3.4 実践：初めての環境を作ってみる

ここまでの知識を使って、実際に環境を作成してみましょう。

### シナリオ

「データ分析プロジェクト」用の環境を作成します。

### ステップ1：プロジェクトフォルダの準備

まず、プロジェクト用のフォルダを作成します。

**Anaconda Promptで実行：**
```bash
cd %USERPROFILE%\Documents\python_projects
mkdir data_analysis_project
cd data_analysis_project
```

### ステップ2：conda環境の作成

```bash
conda create -n data_analysis python=3.11
```

**確認メッセージが出たら `y` を入力してEnter**

### ステップ3：環境のアクティベート

```bash
conda activate data_analysis
```

プロンプトが `(data_analysis)` に変わることを確認。

### ステップ4：環境の確認

```bash
# 環境一覧を表示
conda env list

# 現在の環境のPythonバージョンを確認
python --version
```

出力例：
```
Python 3.11.5
```

### ステップ5：VS Codeで開く

1. VS Codeを起動
2. 「ファイル」→「フォルダーを開く」
3. `data_analysis_project` フォルダを選択
4. 右下のステータスバーをクリック
5. `Python 3.11.5 ('data_analysis': conda)` を選択
6. ターミナルを開く（`` Ctrl + ` ``）
7. プロンプトに `(data_analysis)` と表示されることを確認

**これで環境構築完了です！**

### ステップ6：テストスクリプトを作成

環境が正しく動作するか確認してみましょう。

1. VS Codeのエクスプローラーで「新しいファイル」をクリック
2. ファイル名を `test.py` にする
3. 以下のコードを入力：

```python
import sys

print("Python version:")
print(sys.version)
print("\nConda environment:")
print(sys.prefix)
```

4. ファイルを保存（`Ctrl + S`）
5. 実行する：
   - 方法1：右上の再生ボタン（▶）をクリック
   - 方法2：ターミナルで `python test.py` と入力

**出力例：**
```
Python version:
3.11.5 (main, Sep 11 2023, 13:54:46) [GCC 11.2.0]

Conda environment:
/Users/username/miniconda3/envs/data_analysis
```

環境のパスに `data_analysis` が含まれていれば成功です！

---

## よくあるエラーと対処法

### エラー1：「CondaValueError: prefix already exists」

**エラーメッセージ：**
```
CondaValueError: prefix already exists: /path/to/env/myproject
```

**原因：**
同じ名前の環境がすでに存在している

**対処法：**
```bash
# 既存の環境を削除してから作り直す
conda env remove -n myproject
conda create -n myproject python=3.11

# または、別の名前で作成する
conda create -n myproject_v2 python=3.11
```

### エラー2：「conda activate」が動かない（Windows）

**症状：**
```
'conda' は、内部コマンドまたは外部コマンド、
操作可能なプログラムまたはバッチ ファイルとして認識されていません。
```

**原因：**
Anaconda Promptではなく、通常のコマンドプロンプトを使っている

**対処法：**
- スタートメニューから「Anaconda Prompt (miniconda3)」を起動する

### エラー3：環境をアクティベートしたのにVS Codeで認識されない

**症状：**
- ターミナルでは `(myproject)` と表示される
- でもVS Codeの右下は `('base': conda)` のまま

**原因：**
VS Codeのインタープリタ選択が間違っている

**対処法：**
1. VS Code右下のPythonバージョン表示をクリック
2. 一覧から正しい環境を選択
3. ターミナルを一度閉じて、新しく開く

### エラー4：「PackagesNotFoundError: The following packages are not available」

**エラーメッセージ：**
```
PackagesNotFoundError: The following packages are not available from current channels:
  - python=3.15
```

**原因：**
指定したPythonバージョンが存在しない

**対処法：**
```bash
# 利用可能なPythonバージョンを確認
conda search python

# 存在するバージョンを指定して再実行
conda create -n myproject python=3.11
```

---

## まとめ

この章では、conda環境の作成と管理方法を学びました：

- ✅ conda環境の仕組みを理解
- ✅ プロジェクトごとに環境を分ける重要性を理解
- ✅ `conda create` コマンドで環境を作成
- ✅ `conda activate` / `conda deactivate` で環境を切り替え
- ✅ VS Codeで環境を選択する方法
- ✅ 実際に環境を作って動作確認

**重要なポイントの再確認：**
1. base環境には何もインストールしない
2. プロジェクトごとに新しい環境を作る
3. 作業前に必ず環境をアクティベート
4. プロンプトの `()` 内を常に確認

次の章では、実際にPythonスクリプトを作成して実行します。

---

## 確認問題

1. base環境と個別環境の違いは何ですか？
2. プロジェクトごとに環境を分ける最大のメリットは何ですか？
3. 環境を作成するコマンドは何ですか？（Python 3.11を指定して）
4. 環境をアクティベートするコマンドは何ですか？
5. VS Codeで、現在どの環境が選択されているかを確認する方法は？

---

**前の章へ：** [第2章：環境構築](./第2章_環境構築.md)
**次の章へ：** [第4章：初めてのPythonスクリプト](./第4章_初めてのPythonスクリプト.md)
