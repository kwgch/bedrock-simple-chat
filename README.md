# Bedrock Simple Chat

以下のハンズオンで利用するコードをまとめたリポジトリです。

[【AWSコンテナ入門】簡単なPythonアプリをECSにデプロイしてみよう！](https://qiita.com/minorun365/items/84bef6f06e450a310a6a)

## ここから追記
### copilotでのdeploy
- [1-3. DynamoDBのテーブル作成](https://qiita.com/minorun365/items/84bef6f06e450a310a6a#1-3-dynamodb%E3%81%AE%E3%83%86%E3%83%BC%E3%83%96%E3%83%AB%E4%BD%9C%E6%88%90) は実施しておくこと
- [aws cli install](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html)
- aws cli configure
  ```
  $ aws configure 
  AWS Access Key ID [None]: xxxx
  AWS Secret Access Key [None]: xxxxxx
  Default region name [None]: ap-northeast-1
  Default output format [None]: json
  ```
- [colipot cli install](https://aws.github.io/copilot-cli/ja/docs/getting-started/install)
- copilot初期化
  ```
  $ copilot init \
    -a bsc \
    -n bsc \
    -d ./Dockerfile \
    -t "Load Balanced Web Service" \
    -e dev  \
    --port 8501
  ```
- ecsのタスクロールに以下のポリシーを追加
  - AmazonBedrockFullAccess
  - AmazonDynamoDBFullAccess
- cleanup
  ```
  $ copilot app delete
  ```
- github codespaceでローカル実行する場合のコマンド
  ``` 
  $ python -m streamlit run  main.py
  ```
