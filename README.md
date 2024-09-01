# Bedrock Simple Chat

以下のハンズオンで利用するコードをまとめたリポジトリです。

[【AWSコンテナ入門】簡単なPythonアプリをECSにデプロイしてみよう！](https://qiita.com/minorun365/items/84bef6f06e450a310a6a)

## ここから追記
### copilotでのdeploy
- github上で「.」押してcodespaceで実行するのが速い
- 下記手順は実施しておくこと
  - [1-1. AWSアカウント・IAMユーザーの作成](https://qiita.com/minorun365/items/84bef6f06e450a310a6a#1-1-aws%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88iam%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E3%81%AE%E4%BD%9C%E6%88%90) 
  - [1-2. Bedrockのモデル有効化](https://qiita.com/minorun365/items/84bef6f06e450a310a6a#1-2-bedrock%E3%81%AE%E3%83%A2%E3%83%87%E3%83%AB%E6%9C%89%E5%8A%B9%E5%8C%96)
  - [1-3. DynamoDBのテーブル作成](https://qiita.com/minorun365/items/84bef6f06e450a310a6a#1-3-dynamodb%E3%81%AE%E3%83%86%E3%83%BC%E3%83%96%E3%83%AB%E4%BD%9C%E6%88%90) 
- [aws cli install](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html)
- aws cli configure
  ```
  $ aws configure 
  AWS Access Key ID [None]: xxxx
  AWS Secret Access Key [None]: xxxxxx
  Default region name [None]: ap-northeast-1
  Default output format [None]: json
  ```
  - `AWS Access Key ID`、`AWS Secret Access Key` は「1-1. AWSアカウント・IAMユーザーの作成」で作成したものを入力
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
- デプロイが終わったらWEBページにはアクセスできる。が、会話しようとすると権限が足りずに実行時エラーとなる
- ecsのタスクロールにポリシーを追加（これで会話が可能になる）
  - ecsのタスクロール名を確認（`taskRoleArn` の `:role`/の後ろ。下記例なら `bsc-dev-bsc-TaskRole-xxxxxxxxxxxx`）
    ```
    $ aws ecs describe-task-definition --task-definition `aws ecs list-task-definitions | jq -r '.taskDefinitionArns[0]'` | grep taskRole
        "taskRoleArn": "arn:aws:iam::123456789012:role/bsc-dev-bsc-TaskRole-xxxxxxxxxxxx",
    ```
  - AmazonBedrockFullAccess を追加
    ```
    $ aws iam attach-role-policy --role-name <上記で確認したecsのタスクロール名> --policy-arn arn:aws:iam::aws:policy/AmazonBedrockFullAccess
    ```
  - AmazonDynamoDBFullAccess を追加
    ```
    $ aws iam attach-role-policy --role-name <上記で確認したecsのタスクロール名> --policy-arn arn:aws:iam::aws:policy/AmazonDynamoDBFullAccess
    ```
- 使用を終了するときは下記コマンドを実行
  ```
  $ copilot app delete
  ```
- [参考] github codespaceでローカル実行する場合のコマンド
  ``` 
  $ python -m streamlit run  main.py
  ```
