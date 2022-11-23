# Cloud9の環境構築
今回は全員が同じ環境でハンズオンができるようにCloud9を使って行います。

## Cloud９のインスタンス作成
- AWSのマネジメントコンソールを開き、**東京リージョン**であることを確認します。
- 検索バーに`cloud9`と入力すると、サービス欄にCloud9が表示されるので選択します。

![cloud9_1](./img/cloud9_1.png)

- 画面から`Create environment`を選択します。

![cloud9_2](./img/cloud9_2.png)

- Cloud9の環境構築をしていきます。まず`Details`項目の`Name`には **hanson** と入力します。残りの`Description`と `Environment type`についてはそのままでよいです。

![cloud9_3](./img/cloud9_3.png)

- EC2のインスタンスタイプは**`t3.small`**を選択します。残りの`Platform`と`Timeout`はそのままでよいです。

![cloud9_4](./img/cloud9_4.png)

- Networkについては`Connection`は`AWS Systems Manager (SSM)`になっていればそのままでよいです。`VPC settings`は[作成したVPC](vpc.md#create_vpc)とSubnetを明示的に選択するようにします。

![cloud9_5](./img/cloud9_5.png)

- ここまでの設定が完了したら、画面の下にある`Create`ボタンを押してください。

![cloud9_6](./img/cloud9_6.png)


## クレデンシャル無効化
Cloud9を開いたときに発行される一時認証情報が発行されますが、今回はAmplifyで発行される認証情報を使用するためCloud9側の認証情報の発行を無効化します。

- Cloud9ボタンを押し、`Preference`を選択します。

![cloud9_7](./img/cloud9_7.png)

- `AWS Setting`を選択します。

![cloud9_8](./img/cloud9_8.png)

- `AWS managed temporary credentials`をオフにします

![cloud9_9](./img/cloud9_9.png)

## EBSのボリュームを上げる
デフォルトのままではEBSのボリュームが不足してしまう可能性があるので容量をあげます。

- 現状の容量を確認します。Cloud9のターミナルで以下のコマンドを実行してください。

```
df -h
```

![cloud9_10](./img/cloud9_10.png)

- EBSのsizeが現状10Gなのを確認したら、32Gに増やすためにEBSの設定を変更します。
- Cloud9ボタンを押し、`Go To Your Dashboard`を選択します。

![cloud9_11](./img/cloud9_11.png)

- 作成したCloud9環境を選択します。

![cloud9_12](./img/cloud9_12.png)

- `Manage EC2 instance`を選択します。

![cloud9_13](./img/cloud9_13.png)

- EC2インスタンスの一覧画面が表示されるので、Cloud9のインスタンスIDを選択します。

![cloud9_14](./img/cloud9_14.png)

- EBSのボリュームを変更する場合はインスタンスを停止している必要があるので、`インスタンスの状態`からインスタンスを停止します。

![cloud9_15](./img/cloud9_15.png)

- 確認画面が表示されるので停止ボタンを押します。

![cloud9_16](./img/cloud9_16.png)

- 停止後に同じ画面でストレージタブを押し、ボリュームIDを選択します。

![cloud9_17](./img/cloud9_17.png)

- EBS一覧の中で指定したボリュームIDを選択し、`アクション`ボタンから`ボリュームの変更`を選択します。

![cloud9_18](./img/cloud9_18.png)

- サイズを`32`に変更して`変更`ボタンを押します。

![cloud9_19](./img/cloud9_19.png)

- 確認画面が表示されるので変更ボタンを押します。

![cloud9_20](./img/cloud9_20.png)

- 再度Cloud9に戻り、ボリュームのsizeが増えている事が確認できたらEBSの設定は完了です。

```
df -h
```

![cloud9_21](./img/cloud9_21.png)

ここまででCloud9の環境構築は完了です。