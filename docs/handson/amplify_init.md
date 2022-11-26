# Amplifyの設定
環境準備と使用するアプリケーションが準備できたので、Amplifyの準備をしていきます。  

## 初期設定
**react-amplified**のディレクトリ内で以下のコマンドを実行してください。  

```
amplify init
```

`Enter a name for the project (reactamplified)`と問われるのですが、**入力値はなし**でそのままEnterを押します。  
プロジェクト名には`reactamplified`のデフォルトが表示され、以下のようにAmplifyの設定が表示されます。
`Initialize the project with the above configuration? `とこの設定のまますすめるかを問われるので `y` で進めていきます。  

```shell
$ amplify init
Note: It is recommended to run this command from the root of your app directory
? Enter a name for the project reactamplified
The following configuration will be applied:

Project information
| Name: reactamplified
| Environment: dev
| Default editor: Visual Studio Code
| App type: javascript
| Javascript framework: react
| Source Directory Path: src
| Distribution Directory Path: build
| Build Command: npm run-script build
| Start Command: npm run-script start

? Initialize the project with the above configuration? (Y/n) y
```

次に認証方法を問われます。
Cloud9の設定時にprofileを作成しているため、**AWS profile**を選択します。

```shell
? Initialize the project with the above configuration? Yes
Using default provider  awscloudformation
? Select the authentication method you want to use: (Use arrow keys)
❯ AWS profile 
  AWS access keys 
```

次にprofileの名称を聞かれます、作成したprofileは**default**なので**default**を選択します。

```shell
? Initialize the project with the above configuration? Yes
Using default provider  awscloudformation
? Select the authentication method you want to use: AWS profile

For more information on AWS Profiles, see:
https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html

? Please choose the profile you want to use (Use arrow keys)
❯ default 
```

必要なAWSリソースとリソースを管理するCloudFormationが作成されていきます。  
```
Adding backend environment dev to AWS Amplify app: d1m0h4inkb766a

Deployment completed.
Deployed root stack reactamplified [ ======================================== ] 4/4
        amplify-reactamplified-dev-64… AWS::CloudFormation::Stack     CREATE_COMPLETE                Sat Nov 26 2022 06:49:37…     
        AuthRole                       AWS::IAM::Role                 CREATE_COMPLETE                Sat Nov 26 2022 06:49:35…     
        UnauthRole                     AWS::IAM::Role                 CREATE_COMPLETE                Sat Nov 26 2022 06:49:35…     
        DeploymentBucket               AWS::S3::Bucket                CREATE_COMPLETE                Sat Nov 26 2022 06:49:29…     

? Help improve Amplify CLI by sharing non sensitive configurations on failures (y/N) ‣ 
```

最後に`Help improve Amplify CLI by sharing non sensitive configurations on failures `とAmplifyCLIに何かあったときに情報共有をするか問われますが、デフォルトの*N*のままで進めます。  

```shell
✔ Help improve Amplify CLI by sharing non sensitive configurations on failures (y/N) · no
Deployment bucket fetched.
✔ Initialized provider successfully.
✅ Initialized your environment successfully.

Your project has been successfully initialized and connected to the cloud!

Some next steps:
"amplify status" will show you what you've added already and if it's locally configured or deployed
"amplify add <category>" will allow you to add features like user login or a backend API
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify console" to open the Amplify Console and view your project status
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

Pro tip:
Try "amplify add api" to create a backend API and then "amplify push" to deploy everything
```

これでAmplifyの初期設定は完了です。
