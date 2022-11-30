# APIの追加
Reactのアプリケーションを作成し、新しいAmplifyプロジェクトとして初期化をしたので次は機能追加をしていきます。

## APIの追加
GraphQLのAPIを追加します。  
以下のコマンドをCloud9のターミナルで実行してください。  

```
cd ~/environment/react-amplified; amplify add api
```

REST APIまたはGraphQLかを問われるので、今回のハンズオンでは**GraphQL**を選択します。  
```
? Select from one of the below mentioned services: (Use arrow keys)
❯ GraphQL 
  REST 
```

次の質問は**Continue**を選択します。  
```
? Here is the GraphQL API that we will create. Select a setting to edit or continue (Use arrow keys)
  Name: reactamplified 
  Authorization modes: API key (default, expiration time: 7 days from now) 
  Conflict detection (required for DataStore): Disabled 
❯ Continue 
```

テンプレートになるスキーマを選択できるので、`Single object with fields (e.g., “Todo” with ID, name, description)`を選択します。  
```
? Choose a schema template: (Use arrow keys)
❯ Single object with fields (e.g., “Todo” with ID, name, description) 
  One-to-many relationship (e.g., “Blogs” with “Posts” and “Comments”) 
  Blank Schema 
```

ここまででスキーマ作成は完了します、すぐにスキーマを修正するか問われますが、Cloud9だと開けなかったので一旦**n**で終わらせます。

```
$ amplify add api
? Select from one of the below mentioned services: GraphQL
? Here is the GraphQL API that we will create. Select a setting to edit or continue Continue
? Choose a schema template: Single object with fields (e.g., “Todo” with ID, name, description)

⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema
? Do you want to edit the schema now? (Y/n) ‣ 
```

閉じたあと、**/react-amplified/amplify/backend/api/reactamplified/schema.graphql**にあるschemaファイルが出来ていることを確認します。  

```schema.graphql
type Todo @model {
  id: ID!
  name: String!
  description: String
}
```

直接利用することはありませんが、このスキーマファイルをもとに**AppSync**にAPIが作成されます。  


## APIのデプロイ
作成したスキーマをデプロイするには以下のコマンドを実行します。

```
cd ~/environment/react-amplified; amplify push
```

その後に何度か質問があるのでそれぞれ答えていきます。  

```
✅ GraphQL schema compiled successfully.

Edit your schema at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema.graphql or place .graphql files in a directory at /home/ec2-user/environment/react-amplified/amplify/backend/api/reactamplified/schema

    Current Environment: dev
    
┌──────────┬────────────────┬───────────┬───────────────────┐
│ Category │ Resource name  │ Operation │ Provider plugin   │
├──────────┼────────────────┼───────────┼───────────────────┤
│ Api      │ reactamplified │ Create    │ awscloudformation │
└──────────┴────────────────┴───────────┴───────────────────┘

? Are you sure you want to continue? (Y/n) y

~~~~~~~~(処理が流れる)~~~~~~~~~~

? Do you want to generate code for your newly created GraphQL API (Y/n) y
? Choose the code generation language target (Use arrow keys)
❯ javascript 
  typescript 
  flow 
? Enter the file name pattern of graphql queries, mutations and subscriptions (src/graphql/**/*.js)  (未入力でEnter)
? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions (Y/n) y 
? Enter maximum statement depth [increase from default if your schema is deeply nested] (2)   (未入力でEnter)
```

全ての質問に答えるとAPIがデプロイされていきます。  

```
Deployment completed.
Deployed root stack reactamplified [ ======================================== ] 2/2
        amplify-reactamplified-dev-15… AWS::CloudFormation::Stack     UPDATE_COMPLETE                Sat Nov 26 2022 17:00:35…     
        apireactamplified              AWS::CloudFormation::Stack     CREATE_COMPLETE                Sat Nov 26 2022 17:00:32…     
Deployed api reactamplified [ ======================================== ] 6/6
        GraphQLAPI                     AWS::AppSync::GraphQLApi       CREATE_COMPLETE                Sat Nov 26 2022 16:57:38…     
        GraphQLAPIDefaultApiKey215A6D… AWS::AppSync::ApiKey           CREATE_COMPLETE                Sat Nov 26 2022 16:57:43…     
        GraphQLAPITransformerSchema3C… AWS::AppSync::GraphQLSchema    CREATE_COMPLETE                Sat Nov 26 2022 16:58:43…     
        GraphQLAPINONEDS95A13CF0       AWS::AppSync::DataSource       CREATE_COMPLETE                Sat Nov 26 2022 16:57:42…     
        Todo                           AWS::CloudFormation::Stack     CREATE_COMPLETE                Sat Nov 26 2022 17:00:03…     
        CustomResourcesjson            AWS::CloudFormation::Stack     CREATE_COMPLETE                Sat Nov 26 2022 17:00:18…     

✔ Generated GraphQL operations successfully and saved at src/graphql


GraphQL endpoint: https://q4eq2xymvncejcpplpws5gktmq.appsync-api.ap-northeast-1.amazonaws.com/graphql
GraphQL API KEY: *****************************

GraphQL transformer version: 2

```

デプロイが完了すると**src**ディレクトリ直下に**graphql**というディレクトリが出来ます。  
その中にQueriesやMutationsといったGraphQL用のファイルが出来ています。  
この段階で**AppSync**と**DynamoDB**にもリソースが出来上がっているので、APIとして使えるようになってます。  

ここまででAPI Serverとしての部分は完了になります。