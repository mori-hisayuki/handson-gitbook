# 作成したアプリケーションのホスティング
ここまでで作成したTodoアプリケーションを実際にWeb上に公開するためにホスティングをします。  

## アプリケーションをHostingの設定に追加する
以下のコマンドをCloud9のターミナルで実行してください。  
```
cd ~/environment/react-amplified; amplify add hosting
```

どのサービスを利用してホスティングするかを問われるので**Hosting with Amplify Console**を選択します。  
```
? Select the plugin module to execute …  (Use arrow keys or type to filter)
❯ Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
  Amazon CloudFront and S3
```

次にデプロイ方法について問われます、今回のハンズオンではマニュアルでのデプロイにします。  
```
? Choose a type (Use arrow keys)
  Continuous deployment (Git-based deployments) 
❯ Manual deployment 
  Learn more 
```

以下の表示がされたらホスティングの設定追加が完了です。

```
You can now publish your app using the following command:

Command: amplify publish
```

**amplify status**コマンドで確認をします。

```
$ amplify status

    Current Environment: dev
    
┌──────────┬────────────────┬───────────┬───────────────────┐
│ Category │ Resource name  │ Operation │ Provider plugin   │
├──────────┼────────────────┼───────────┼───────────────────┤
│ Hosting  │ amplifyhosting │ Create    │ awscloudformation │
├──────────┼────────────────┼───────────┼───────────────────┤
│ Api      │ reactamplified │ No Change │ awscloudformation │
└──────────┴────────────────┴───────────┴───────────────────┘

GraphQL endpoint: https://q4eq2xymvncejcpplpws5gktmq.appsync-api.ap-northeast-1.amazonaws.com/graphql
GraphQL API KEY: *********************************

GraphQL transformer version: 2

No amplify console domain detected
```

API以外にHostingが追加されていることがわかります。  

## アプリケーションのPublishを行う
amplifyに対してHosting設定を追加したので、次は実際にWeb上に公開します。  
以下のコマンドをCloud9のターミナルで実行してください。  
```
cd ~/environment/react-amplified; amplify publish
```

リソースに特に問題がなければ**y**で先に進みます。
```
✔ Successfully pulled backend environment dev from the cloud.

    Current Environment: dev
    
┌──────────┬────────────────┬───────────┬───────────────────┐
│ Category │ Resource name  │ Operation │ Provider plugin   │
├──────────┼────────────────┼───────────┼───────────────────┤
│ Hosting  │ amplifyhosting │ Create    │ awscloudformation │
├──────────┼────────────────┼───────────┼───────────────────┤
│ Api      │ reactamplified │ No Change │ awscloudformation │
└──────────┴────────────────┴───────────┴───────────────────┘
? Are you sure you want to continue? (Y/n) y
```

リソースの更新や足りないリソースの作成などを行われます。  
最後に**Deployment complete**表示されたらホスティングが完了となります。  

```
Deployment completed.
Deployed root stack reactamplified [ ======================================== ] 3/3
        amplify-reactamplified-dev-15… AWS::CloudFormation::Stack     UPDATE_COMPLETE                Sun Nov 27 2022 05:27:45…     
        hostingamplifyhosting          AWS::CloudFormation::Stack     CREATE_COMPLETE                Sun Nov 27 2022 05:27:19…     
        apireactamplified              AWS::CloudFormation::Stack     UPDATE_COMPLETE                Sun Nov 27 2022 05:27:30…     
Deployed hosting amplifyhosting [ ======================================== ] 1/1
        AmplifyBranch                  AWS::Amplify::Branch           CREATE_IN_PROGRESS             Sun Nov 27 2022 05:27:12…     



GraphQL transformer version: 2

Publish started for amplifyhosting

> react-amplified@0.1.0 build
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  168.91 kB  build/static/js/main.7537560b.js
  1.79 kB    build/static/js/787.cbb326c1.chunk.js
  264 B      build/static/css/main.e6c13ad2.css

The project was built assuming it is hosted at /.
You can control this with the homepage field in your package.json.

The build folder is ready to be deployed.
You may serve it with a static server:

  npm install -g serve
  serve -s build

Find out more about deployment here:

  https://cra.link/deployment

✔ Zipping artifacts completed.
✔ Deployment complete!
https://dev.dat6043122agk.amplifyapp.com
```

最後に表示されているURLにアクセスして、ここまでに作ったアプリケーションが表示されるかを確認してみてください。  
ToDoの作成も問題なく出来たらハンズオンは完了となります。
