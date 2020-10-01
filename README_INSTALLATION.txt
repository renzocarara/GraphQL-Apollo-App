>vue create vue-graphql (seleionar Vue 2, Vue 3 sembra avere al momento qualche incompatibilità con Apollo)
 Default ([Vue 2] babel, eslint)
 Default (Vue 3 Preview) ([Vue 3] babel, eslint)
 Manually select features


///////////////////////////////////////////////// APOLLO ///////////////////////////////////////////////////////////////////////
>vue add apollo
? Add example code No
? Add a GraphQL API Server? No
? Configure Apollo Engine? No

modificare il file vue-apollo.js, le seguenti 2 linee
  process.env.VUE_APP_GRAPHQL_HTTP || "http://localhost:4000/helloworld";
  process.env.VUE_APP_GRAPHQL_WS || "ws://localhost:4000/helloworld",
bisogna inserirci l'url del graphQL server

Nel componente che usa la API graphQL
inserire la proprietà "apollo", all'interno della quale scriveremo la query
e fare l'import (come indicato sul sito https://apollo.vuejs.org/guide/apollo/#apollo-options)

///////////////////////////////////////////////// PRISMA ///////////////////////////////////////////////////////////////////////

installo globalmente prisma:
> npm install -g prisma

npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
npm WARN deprecated graphql-import@0.7.1: GraphQL Import has been deprecated and merged into GraphQL Tools, so it will no longer get updates. Use GraphQL Tools instead to stay up-to-date! Check out https://www.graphql-tools.com/docs/migration-from-import for migration and https://the-guild.dev/blog/graphql-tools-v6 for new changes.
C:\Users\renzo\AppData\Roaming\npm\prisma -> C:\Users\renzo\AppData\Roaming\npm\node_modules\prisma\dist\index.js
+ prisma@1.34.10
added 595 packages from 485 contributors in 118.692s

installo graphql-cli:
> npm install -g graphql-cli

npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated har-validator@5.1.5: this library is no longer supported
C:\Users\renzo\AppData\Roaming\npm\graphql -> C:\Users\renzo\AppData\Roaming\npm\node_modules\graphql-cli\dist\bin.js


creo una nuova cartella dove metterò il mio server e inizializzo il server
(qui sotto potrei avere anche un altra cartella client.... nel caso)
> mkdir startrek
> cd .\startrek\
> prisma init server

? Set up a new Prisma server or deploy to an existing server? Demo server + MySQL database
Opening https://app.prisma.io/cli-auth?secret=$2a$08$.DTXwuReQW7PL8yY5Wjruu in the browser

Authenticating √
Authenticated with renzo.carara@libero.it
? Choose the region of your demo server renzo-carara/demo-eu1
? Choose a name for your service startrek
? Choose a name for your stage dev                                                   quires login)
? Select the programming language for the generated Prisma client NONE

Created 2 new files:

  prisma.yml           Prisma service definition
  datamodel.prisma    GraphQL SDL-based datamodel (foundation for database)

Next steps:

  1. Open folder: cd server
  2. Deploy your Prisma service: prisma deploy
  3. Read more about deploying services:
     http://bit.ly/prisma-deploy-services

Generating schema... 19ms

PS D:\SVILUPPO\graphQL\prismy> cd server
PS D:\SVILUPPO\graphQL\prismy\server> ls

    Directory: D:\SVILUPPO\graphQL\prismy\server

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        29/09/2020     19:16             44 datamodel.prisma
-a----        29/09/2020     19:16            167 prisma.yml


deployo il server, dalla cartella server
>deploy server
ottengo:
Creating stage dev for service prismy1 √
Deploying service `startrek` to stage `dev` to server `prisma-eu1` 341ms

Changes:

  User (Type)
  + Created type `User`
  + Created field `id` of type `ID!`
  + Created field `name` of type `String!`

Applying changes 1.3s
Generating schema 24ms
Saving Prisma Client (JavaScript) at D:\SVILUPPO\graphQL\startrek\server\generated\prisma-client\

Your Prisma endpoint is live:

  HTTP:  https://eu1.prisma.sh/renzo-carara/startrek/dev
  WS:    wss://eu1.prisma.sh/renzo-carara/startrek/dev

You can view & edit your data here:

  Prisma Admin: https://eu1.prisma.sh/renzo-carara/startrek/dev/_admin

All'indirizzo qui sopra posso aggiungere dei record al mio DB
(vedi: https://v1.prisma.io/docs/1.34/prisma-admin/overview-el3e/)



Qunando voglio re-deployare, perchè ho cambiato qualcosa nel datamodel.prisma,
ma ho già un database con dei dati inseriti,
devo usare l'opzione "--force" ma perderò tutti i dati contenuti nel DB!!!

>prisma deploy --force



OPZIONALE: invece che dal browser posso accedere tramite CLI
installo e faccio login su prisma1 CLI
>npm install -g prisma1
>prisma1 login -k eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOiJja2ZvODBhZjYyeTY1MDg2MXR5dHozam44IiwiaWF0IjoxNjAxNDUxNTgxLCJleHAiOjE2MDQwNDM1ODF9.yD_KtY065UMfpDUgM4_Sh2T3KADwsGtVpZDZTi33XsE

/////////////////////////////////// NOTE /////////////////////////////////////////
The first thing you should understand is that the Prisma layer acts as an ORM (i.e. like Sequelize)
 you don’t directly interact with the database with SQL queries.
 All of the types, inputs, mutations, and queries in the Prisma layer are automatically
 generated from the Prisma datamodel you define and are required to create/modify data in the database.

 datamodel.prisma file:
 is where you will define all of the types which will define how 
 the data and relationships look in the database.
  The types in this file would look like the types in a GraphQL schema file
  (all the types minus the queries, mutations or subscriptions).

  The index.js/schema.graphql in the src folder is where you define the public-facing part to the API.
   The schema.graphql is like a standard GraphQL schema defining all the types
   and the index.js in the src folder is where you start the server and define resolvers.


