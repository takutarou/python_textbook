# 付録A：よく使うcondaコマンド一覧（Windows版）

このページでは、Windows環境で日常的に使用するcondaコマンドを体系的にまとめています。
困った時にすぐ参照できるリファレンスとして活用してください。

**実行環境：** Anaconda Prompt (miniconda3)

---

## 目次

1. [環境管理系コマンド](#環境管理系コマンド)
2. [パッケージ管理系コマンド](#パッケージ管理系コマンド)
3. [情報確認系コマンド](#情報確認系コマンド)
4. [その他の便利なコマンド](#その他の便利なコマンド)
5. [よく使うオプション](#よく使うオプション)
6. [トラブルシューティング用コマンド](#トラブルシューティング用コマンド)

---

## 環境管理系コマンド

### 環境を作成する

```bash
# 基本形（Pythonバージョン指定）
conda create -n 環境名 python=3.11

# 例
conda create -n myproject python=3.11
```

**同時にパッケージもインストール：**
```bash
conda create -n myproject python=3.11 pandas numpy matplotlib
```

### 環境を削除する

```bash
conda env remove -n 環境名

# 例
conda env remove -n myproject
```

**確認メッセージなしで削除：**
```bash
conda env remove -n myproject -y
```

### 環境の一覧を表示する

```bash
conda env list
```

または

```bash
conda info --envs
```

**出力例：**
```
# conda environments:
#
base                  *  C:\Users\username\miniconda3
myproject                C:\Users\username\miniconda3\envs\myproject
data_analysis            C:\Users\username\miniconda3\envs\data_analysis
```

`*` がついているのが現在アクティブな環境

### 環境をアクティベートする

```bash
conda activate 環境名

# 例
conda activate myproject
```

**プロンプトが変わる：**
```bash
# 変更前
(base) C:\Users\username>

# 変更後
(myproject) C:\Users\username>
```

### 環境をデアクティベートする

```bash
conda deactivate
```

base環境に戻ります。

### 環境を複製する

```bash
conda create -n 新環境名 --clone 元環境名

# 例：myprojectをmyproject_backupとして複製
conda create -n myproject_backup --clone myproject
```

### 環境をエクスポートする

```bash
# environment.ymlファイルとして保存
conda env export > environment.yml
```

**保存場所を指定：**
```bash
conda env export > C:\Users\username\Documents\environment.yml
```

### 環境をインポートする

```bash
# environment.ymlから環境を再現
conda env create -f environment.yml
```

**別の場所のファイルから：**
```bash
conda env create -f C:\Users\username\Documents\environment.yml
```

---

## パッケージ管理系コマンド

### パッケージをインストールする

```bash
# 基本形
conda install パッケージ名

# 例
conda install pandas
```

**複数のパッケージを一度にインストール：**
```bash
conda install pandas numpy matplotlib
```

**特定のバージョンを指定：**
```bash
conda install pandas=2.0.0
```

**conda-forgeチャンネルから：**
```bash
conda install -c conda-forge パッケージ名

# 例
conda install -c conda-forge openpyxl
```

**確認メッセージなしでインストール：**
```bash
conda install pandas -y
```

### パッケージをアンインストールする

```bash
conda uninstall パッケージ名

# 例
conda uninstall pandas
```

または

```bash
conda remove パッケージ名
```

### パッケージをアップデートする

```bash
# 特定のパッケージを更新
conda update パッケージ名

# 例
conda update pandas
```

**すべてのパッケージを更新（注意）：**
```bash
conda update --all
```

**conda自体を更新：**
```bash
conda update conda
```

### インストール済みパッケージの一覧

```bash
# すべてのパッケージを表示
conda list
```

**出力例：**
```
# packages in environment at C:\Users\username\miniconda3\envs\myproject:
#
# Name                    Version                   Build  Channel
numpy                     1.24.3          py311h1234567_0
pandas                    2.0.3           py311h1234567_0
python                    3.11.5               h1234567_0
```

**特定のパッケージを検索（Windows）：**
```bash
conda list | findstr pandas
```

### パッケージを検索する

```bash
# 利用可能なバージョンを検索
conda search パッケージ名

# 例
conda search pandas
```

**conda-forgeチャンネルで検索：**
```bash
conda search -c conda-forge パッケージ名
```

---

## 情報確認系コマンド

### condaのバージョン確認

```bash
conda --version
```

または

```bash
conda -V
```

**出力例：**
```
conda 24.1.2
```

### conda全体の情報表示

```bash
conda info
```

**出力内容：**
- condaバージョン
- Pythonバージョン
- プラットフォーム（Windows）
- 環境のパス
- チャンネル設定

### 現在の環境情報

プロンプトの `()` 内を見るのが最も簡単：
```bash
(myproject) C:\Users\username>  # myproject環境がアクティブ
```

### Pythonバージョン確認

```bash
python --version
```

または

```bash
python -V
```

### 現在のディレクトリ確認

```bash
cd
```

**出力例：**
```
C:\Users\username\Documents\python_projects\myproject
```

---

## その他の便利なコマンド

### キャッシュのクリア

```bash
# 未使用のパッケージとキャッシュを削除
conda clean --all
```

**確認メッセージなし：**
```bash
conda clean --all -y
```

**パッケージキャッシュのみ削除：**
```bash
conda clean --packages
```

### チャンネルの設定

```bash
# conda-forgeを優先チャンネルに追加
conda config --add channels conda-forge

# チャンネルの優先度を厳密に
conda config --set channel_priority strict
```

**設定を確認：**
```bash
conda config --show channels
```

### 設定の表示

```bash
# すべての設定を表示
conda config --show
```

**特定の設定のみ：**
```bash
conda config --show channels
```

---

## よく使うオプション

### 共通オプション

| オプション | 説明 | 例 |
|----------|------|---|
| `-n` または `--name` | 環境名を指定 | `conda install -n myproject pandas` |
| `-y` または `--yes` | 確認メッセージをスキップ | `conda install pandas -y` |
| `-c` または `--channel` | チャンネルを指定 | `conda install -c conda-forge openpyxl` |
| `--dry-run` | 実際には実行せず、何が起きるか表示 | `conda install pandas --dry-run` |
| `-q` または `--quiet` | 出力を最小限に | `conda install pandas -q` |
| `-v` または `--verbose` | 詳細な出力 | `conda install pandas -v` |

### 使用例

**dry-runで事前確認：**
```bash
# パッケージをインストールする前に、何がインストールされるか確認
conda install pandas --dry-run
```

**別の環境にパッケージをインストール：**
```bash
# myproject環境にpandasをインストール（環境をアクティベートせずに）
conda install -n myproject pandas
```

---

## トラブルシューティング用コマンド

### 環境が壊れた時

```bash
# 環境を削除して作り直す
conda env remove -n myproject
conda create -n myproject python=3.11
```

### パッケージの依存関係を確認

```bash
# 特定のパッケージが何に依存しているか
conda list パッケージ名 --show-channel-urls
```

### condaの再初期化（Windows）

```bash
conda init cmd.exe
```

**PowerShellの場合：**
```bash
conda init powershell
```

その後、Anaconda Promptを再起動。

### パッケージの整合性チェック

```bash
# 環境の整合性を確認
conda list --revisions
```

### 以前のリビジョンに戻す

```bash
# 環境を以前の状態に戻す
conda install --revision リビジョン番号

# 例：リビジョン3に戻す
conda install --revision 3
```

---

## Windows固有の注意点

### Anaconda Promptの起動

**重要：** 通常のコマンドプロンプトではなく、必ず「Anaconda Prompt (miniconda3)」を使用してください。

**起動方法：**
1. Windowsキーを押す
2. 「Anaconda Prompt」と入力
3. 「Anaconda Prompt (miniconda3)」を選択

### パスの扱い

**Windowsのパス：**
```bash
# バックスラッシュ
C:\Users\username\Documents\data.csv

# スラッシュも使える（推奨）
C:/Users/username/Documents/data.csv
```

### ファイル検索（findstr）

```bash
# 特定のパッケージを検索
conda list | findstr パッケージ名

# 例
conda list | findstr pandas
```

### 環境変数の確認

```bash
# ユーザー環境変数を表示
echo %USERPROFILE%

# 出力例
C:\Users\username
```

---

## クイックリファレンス

### 基本的なワークフロー

```bash
# 1. Anaconda Promptを起動

# 2. 新規プロジェクト開始
conda create -n myproject python=3.11
conda activate myproject

# 3. 必要なパッケージをインストール
conda install pandas numpy matplotlib

# 4. プロジェクトフォルダに移動
cd C:\Users\username\Documents\python_projects\myproject

# 5. 作業する
python script.py

# 6. 作業終了
conda deactivate

# --- 別の日 ---

# 7. Anaconda Promptを起動

# 8. プロジェクト再開
conda activate myproject
cd C:\Users\username\Documents\python_projects\myproject

# 9. 必要に応じてパッケージを追加
conda install openpyxl

# 10. 作業終了
conda deactivate
```

### 環境を他のPCに移す

**PC-A（環境をエクスポート）：**
```bash
conda activate myproject
conda env export > C:\Users\username\Documents\environment.yml
```

USBメモリやクラウドで `environment.yml` を他のPCにコピー

**PC-B（環境をインポート）：**
```bash
conda env create -f C:\Users\username\Documents\environment.yml
conda activate myproject
```

---

## チートシート

### 最もよく使う10コマンド

```bash
# 1. 環境一覧
conda env list

# 2. 環境作成
conda create -n 環境名 python=3.11

# 3. 環境アクティベート
conda activate 環境名

# 4. パッケージインストール
conda install パッケージ名

# 5. パッケージ一覧
conda list

# 6. 特定パッケージの検索
conda list | findstr パッケージ名

# 7. パッケージアンインストール
conda uninstall パッケージ名

# 8. 環境デアクティベート
conda deactivate

# 9. 環境削除
conda env remove -n 環境名

# 10. condaバージョン確認
conda --version
```

---

## 注意事項

### やってはいけないこと

❌ **base環境にパッケージをインストール**
```bash
# これは避ける
(base) C:\Users\username> conda install pandas
```

✅ **専用環境を作ってインストール**
```bash
conda create -n myproject python=3.11
conda activate myproject
conda install pandas
```

❌ **通常のコマンドプロンプトを使う**
```bash
# コマンドプロンプト → conda が認識されない
```

✅ **Anaconda Promptを使う**
```bash
# スタートメニューから「Anaconda Prompt (miniconda3)」
```

❌ **環境をアクティベートせずに作業**
```bash
# プロンプトを確認せずに作業
```

✅ **必ず環境を確認**
```bash
# プロンプトの()内を確認
(myproject) C:\Users\username>  # ← これを確認してから作業
```

---

## VS Codeでcondaを使う場合

### VS Codeターミナルの初期化

初回のみ実行：
```bash
conda init cmd.exe
```

VS Codeを再起動すると、ターミナルで自動的にcondaが使えるようになります。

### VS Codeでの環境確認

ターミナルを開いた時、プロンプトに環境名が表示されることを確認：
```bash
(myproject) PS C:\Users\username\Documents\python_projects\myproject>
```

---

## まとめ

**最も重要なコマンド：**
1. `conda env list` - 環境一覧
2. `conda activate 環境名` - 環境有効化
3. `conda install パッケージ名` - パッケージ追加
4. `conda list | findstr パッケージ名` - パッケージ検索

**困った時：**
1. Anaconda Promptを使っているか確認
2. `conda env list` で現在の環境を確認
3. `conda list` でパッケージを確認
4. `conda clean --all` でキャッシュクリア
5. 最終手段：環境を作り直す

**関連章：**
- [第2章：環境構築](./第2章_環境構築.md)
- [第3章：conda環境の理解と作成](./第3章_conda環境の理解と作成.md)
- [第7章：つまずきポイント集](./第7章_つまずきポイント集.md)

---

**目次に戻る：** [第0章：目次](./第0章_目次.md)
