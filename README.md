# Bedrock Simple Chat

以下のハンズオンで利用するコードをまとめたリポジトリです。

[【AWSコンテナ入門】簡単なPythonアプリをECSにデプロイしてみよう！](https://qiita.com/minorun365/items/84bef6f06e450a310a6a)

## 追記

- aws cli install
  - https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.htmlß
- colipot cli install
  - https://aws.github.io/copilot-cli/ja/docs/getting-started/install

- github codespaceで実行する場合のコマンド
  ``` 
  python -m streamlit run  main.py
  ```
- portを指定してcopilotでdeployする場合のコマンド
  ```
  copilot svc init --name bsc --port 8501
  copilot svc deploy --name bsc --env dev
  ```
- permissionsも指定する場合
  ```
  copilot svc init \
    --name bsc \
    --type "Load Balanced Web Service" \
    --dockerfile ./Dockerfile \
    --port 8501 \
    --permissions "bedrock:*,dynamodb:*"
  ```
- TODO: 上記でdeployできるが実行時エラーが出るので要調査
