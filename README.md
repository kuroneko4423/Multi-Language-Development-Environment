# Multi-Language Development Environment

このワークスペースは、JavaとPythonを中心とした多言語開発環境をDevContainerを使用して提供します。チームメンバー全員が同じ開発環境を構築することで、環境の違いによる問題を解決し、効率的な開発を行うことができます。

## 前提条件

### 1. Visual Studio Code のインストール

[Visual Studio Code公式サイト](https://code.visualstudio.com/)からダウンロードしてインストールしてください。

### 2. Dev Containers 拡張機能のインストール

VSCodeを起動し、以下の手順で拡張機能をインストールしてください：

1. VSCodeの拡張機能タブ（Ctrl+Shift+X）を開く
2. 検索バーに「Dev Containers」と入力
3. Microsoft製の「Dev Containers」拡張機能をインストール

または、以下のリンクから直接インストール：
[Dev Containers - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### 3. Rancher Desktop のインストール

**注意：Docker Desktopではなく、Rancher Desktopを使用してください。**

#### Windows の場合：
1. [Rancher Desktop公式サイト](https://rancherdesktop.io/)にアクセス
2. 「Download for Windows」をクリック
3. ダウンロードしたインストーラーを実行
4. インストール完了後、Rancher Desktopを起動
5. 初回起動時の設定で「dockerd (moby)」を選択（推奨）

#### macOS の場合：
1. [Rancher Desktop公式サイト](https://rancherdesktop.io/)にアクセス
2. 「Download for macOS」をクリック
3. ダウンロードしたdmgファイルをマウントし、アプリケーションフォルダにドラッグ
4. アプリケーションを起動し、初回設定を完了

#### Linux の場合：
1. [Rancher Desktop公式サイト](https://rancherdesktop.io/)にアクセス
2. 「Download for Linux」をクリック
3. 配布形式（AppImage、deb、rpmなど）を選択してダウンロード
4. インストール後、アプリケーションを起動

## 使用方法

### 1. プロジェクトのクローン

```bash
git clone <このリポジトリのURL>
cd <プロジェクトディレクトリ>
```

### 2. DevContainerでの開発環境起動

1. VSCodeでプロジェクトフォルダを開く
2. 右下に表示される「Reopen in Container」の通知をクリック
   
   または
   
   - コマンドパレット（Ctrl+Shift+P / Cmd+Shift+P）を開く
   - 「Dev Containers: Reopen in Container」を選択

3. 初回起動時はコンテナイメージのダウンロードとビルドが行われます（数分かかる場合があります）

### 3. 開発環境の確認

コンテナが起動したら、ターミナルで以下のコマンドを実行して環境を確認してください：

```bash
# Java バージョン確認
java -version

# Python バージョン確認
python --version

# Node.js バージョン確認
node --version

# Maven バージョン確認
mvn --version

# Gradle バージョン確認
gradle --version
```

## 開発環境の詳細

### インストール済み言語・ツール

- **Java 17** (OpenJDK)
  - Maven
  - Gradle
- **Python 3.11**
  - pip (最新版)
  - Django
  - FastAPI
  - Streamlit
  - uvicorn
- **Node.js 18**
  - npm
  - Vue CLI

### プリインストール済みVSCode拡張機能

#### 汎用ツール
- Markdown Preview Enhanced
- Markdown All in One
- Markdown Table
- markdownlint
- PlantUML
- YAML
- Draw.io Integration

#### フロントエンド開発
- HTML Preview
- TypeScript
- Vue Language Features (Volar)
- HTML Language Features

#### Java開発
- Extension Pack for Java
- Spring Boot Dashboard
- Spring Initializr Java Support

#### Python開発
- Python
- Flake8
- Black Formatter
- Django
- Jupyter

#### データベース
- Database Client

#### AI開発支援
- Roo Cline

### ポート転送設定

以下のポートが自動的に転送されます：

- **3000**: Vue.js開発サーバー
- **8000**: Django/FastAPI サーバー
- **8080**: Spring Boot サーバー
- **8501**: Streamlit アプリケーション

## プロジェクト構造

```
.
├── .devcontainer/
│   └── devcontainer.json    # DevContainer設定ファイル
├── java/                    # Javaプロジェクト用ディレクトリ
├── python/                  # Pythonプロジェクト用ディレクトリ
└── README.md               # このファイル
```

## トラブルシューティング

### コンテナが起動しない場合

1. Rancher Desktopが正常に動作していることを確認
2. VSCodeのDev Containers拡張機能が最新版であることを確認
3. コマンドパレットから「Dev Containers: Rebuild Container」を実行

### ポートにアクセスできない場合

1. VSCodeの「PORTS」タブでポートが転送されていることを確認
2. ファイアウォールの設定を確認
3. アプリケーションが正しいポートで起動していることを確認

### パフォーマンスが遅い場合

1. Rancher Desktopのリソース設定（CPU、メモリ）を確認
2. 不要なコンテナやイメージを削除してディスク容量を確保
3. WSL2（Windows）の場合、WSL2の設定を最適化

## 開発の開始

### Javaプロジェクトの場合

```bash
cd java
# Maven プロジェクトの場合
mvn spring-boot:run

# Gradle プロジェクトの場合
gradle bootRun
```

### Pythonプロジェクトの場合

```bash
cd python
# Django プロジェクトの場合
python manage.py runserver 0.0.0.0:8000

# FastAPI プロジェクトの場合
uvicorn main:app --host 0.0.0.0 --port 8000

# Streamlit アプリの場合
streamlit run app.py --server.port 8501 --server.address 0.0.0.0
```

## 注意事項

- 初回起動時はコンテナイメージのダウンロードに時間がかかります
- ファイルの変更はホストマシンとコンテナ間で同期されます
- コンテナを停止してもファイルの変更は保持されます
- 新しいパッケージをインストールした場合、コンテナを再ビルドすることを推奨します

## サポート

問題が発生した場合は、以下を確認してください：

1. [Dev Containers公式ドキュメント](https://code.visualstudio.com/docs/devcontainers/containers)
2. [Rancher Desktop公式ドキュメント](https://docs.rancherdesktop.io/)
3. プロジェクトのIssueページ

---

Happy Coding! 🚀