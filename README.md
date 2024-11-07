Anthropic Computer Use Demo - Docker Compose Setup
===

このリポジトリでは、Anthropicの `computer-use-demo` イメージを使用して、Docker Composeによる環境構築手順を説明します。  
このセットアップにより、環境変数やポート、ボリュームの設定を行った上で、コンテナを簡単に起動できます。  

## 必要条件
- Docker
- Docker Compose

## 手順

### 1. リポジトリをクローンする
まず、このリポジトリをローカル環境にクローンしてください。

```bash
git clone https://github.com/ss-nakano/docker-compose-for-anthropic-quickstarts-computer-use-demo-latest
cd docker-compose-for-anthropic-quickstarts-computer-use-demo-latest
```

### 2. `.env` ファイルの作成
APIキーを環境変数として設定するために、`.env` ファイルを作成します。

1. `.env.example` ファイルを元に `.env` ファイルを作成します。
   ```bash
   cp .env.example .env
   ```

2. `.env` ファイルを編集し、 `your_actual_api_key_here` を実際の `ANTHROPIC_API_KEY` に置き換えて保存します。
   ```env
   ANTHROPIC_API_KEY=your_actual_api_key_here
   ```

※ APIキーについては、[Anthropic Console](https://console.anthropic.com)から取得可能です。


### 3. Docker Compose ファイルの確認
リポジトリ内の `docker-compose.yml` ファイルには、以下の設定が含まれています：
- 必要なポートがホストに公開されるように設定（5900, 8501, 6080, 8080）
- APIキーを環境変数として設定
- ホームディレクトリの `.anthropic` フォルダをコンテナ内にマウント

設定内容を確認し、必要に応じてカスタマイズしてください。

### 4. コンテナの起動
以下のコマンドを実行して、コンテナをバックグラウンドで起動します。

```bash
docker-compose up -d
```

### 5. コンテナの停止
不要になった場合は、以下のコマンドでコンテナを停止および削除できます。

```bash
docker-compose down
```

### 6. 利用開始
[http://localhost:8080](http://localhost:8080)を開くと、エージェントチャットとデスクトップビューの両方が含まれる統合インターフェースを表示することができます。

詳細な利用方法、注意点については、[Anthropics公式のドキュメント](https://github.com/anthropics/anthropic-quickstarts/tree/main/computer-use-demo)を参照してください。



## ファイル構成
- `README.md`：セットアップ手順（本ファイル）
- `docker-compose.yml`：コンテナの設定ファイル
- `.env.example`：APIキーの設定を記述したサンプルファイル
- `.anthropic` :anthropicコンテナへマウントを行うディレクトリ（docker composeコマンドの実行後に自動作成されます）

## 注意
- 実際の `.env` ファイルには、機密情報を含むため、公開しないようにご注意ください。
- ポート設定は公式ドキュメントで示されている内容から変更していません。、必要に応じて `docker-compose.yml` 内で変更できます。

## トラブルシューティング
- **APIキーのエラー**: `.env` ファイル内の `ANTHROPIC_API_KEY` に正しいAPIキーが設定されているか確認してください。
- **ポートの競合**: 他のプロセスで同じポートが使用されている場合、 `docker-compose.yml` のポート設定を変更してください。

---