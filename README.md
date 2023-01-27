# Prisma SQLServer Shadow DB issue

When running `prisma migrate dev` a second time after creating the initial migration, we get the following error:

```sh
Error: P3006

Migration `20230127095507_initial` failed to apply cleanly to the shadow database.
Error:
The specified schema name "myschema" either does not exist or you do not have permission to use it.
   0: migration_core::state::DevDiagnostic
             at migration-engine/core/src/state.rs:269
```

## Steps to reproduce
1. Run the db with `docker-compose up`
2. Run `npm run migrate:dev` to create the initial migration (which is successful)
3. Run `npm run migrate:dev` again resulting in the error mentioned above.


## Detailed error log

```sh
> prisma-sqlserver-shadow-issue@1.0.0 migrate:dev
> DEBUG="*" prisma migrate dev

  prisma:engines  binaries to download libquery-engine, migration-engine, introspection-engine, prisma-fmt +0ms
  prisma:loadEnv  project root found at /Users/joost/git/holi/prisma-sqlserver-shadow-issue/package.json +0ms
  prisma:tryLoadEnv  Environment variables loaded from /Users/joost/git/holi/prisma-sqlserver-shadow-issue/.env +0ms
  prisma:getConfig  Using getConfig Wasm +0ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +1ms
  prisma:loadEnv  project root found at /Users/joost/git/holi/prisma-sqlserver-shadow-issue/package.json +5ms
  prisma:tryLoadEnv  Environment variables loaded from /Users/joost/git/holi/prisma-sqlserver-shadow-issue/.env +4ms
Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma
  prisma:getConfig  Using getConfig Wasm +1ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +1ms
Datasource "db": SQL Server database

  prisma:getDMMF  Using CLI Query Engine (Node-API Library) at: /Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/@prisma/engines/libquery_engine-darwin-arm64.dylib.node +0ms
  prisma:getDMMF  Loaded Node-API Library +2ms
  prisma:getDMMF  unserialized dmmf result ready +1ms
  prisma:getDMMF  dmmf retrieved without errors in getDmmfNodeAPI +1ms
  prisma:getConfig  Using getConfig Wasm +5ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +0ms
  prisma:getConfig  Using getConfig Wasm +0ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +2ms
  prisma:migrateEngine:rpc  starting migration engine with binary: /Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/@prisma/engines/migration-engine-darwin-arm64 +0ms
  prisma:migrateEngine:rpc  SENDING RPC CALL {"id":1,"jsonrpc":"2.0","method":"devDiagnostic","params":{"migrationsDirectoryPath":"/Users/joost/git/holi/prisma-sqlserver-shadow-issue/prisma/migrations"}} +6ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.672656Z","level":"INFO","fields":{"message":"Starting migration engine RPC server","git_hash":"ceb5c99003b99c9ee2c1d2e618e359c14aef2ea5"},"target":"migration_engine"} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.677302Z","level":"INFO","fields":{"message":"Performing a TLS handshake"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +5ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.677323Z","level":"WARN","fields":{"message":"Trusting the server certificate without validation."},"target":"tiberius::client::tls_stream::opentls_tls_stream","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.686689Z","level":"INFO","fields":{"message":"TLS handshake successful"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +9ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.686713Z","level":"WARN","fields":{"message":"Turning TLS off after a login. All traffic from here on is not encrypted."},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.690172Z","level":"INFO","fields":{"message":"Database change from 'mydb' to 'master'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +4ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.690206Z","level":"INFO","fields":{"message":"Changed database context to 'mydb'."},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.690214Z","level":"INFO","fields":{"message":"SQL collation changed to windows-1252"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.690218Z","level":"INFO","fields":{"message":"Microsoft SQL Server\u0000\u0000 version 3892510736"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.690222Z","level":"INFO","fields":{"message":"Packet size change from '4096' to '4096'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.829757Z","level":"INFO","fields":{"message":"Performing a TLS handshake"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +139ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.829779Z","level":"WARN","fields":{"message":"Trusting the server certificate without validation."},"target":"tiberius::client::tls_stream::opentls_tls_stream","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.83886Z","level":"INFO","fields":{"message":"TLS handshake successful"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +9ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.838892Z","level":"WARN","fields":{"message":"Turning TLS off after a login. All traffic from here on is not encrypted."},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +1ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.841781Z","level":"INFO","fields":{"message":"Database change from 'prisma_migrate_shadow_db_7d18cea3-c3a5-4581-bedc-7a3ee5e93968' to 'master'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +2ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.841809Z","level":"INFO","fields":{"message":"Changed database context to 'prisma_migrate_shadow_db_7d18cea3-c3a5-4581-bedc-7a3ee5e93968'."},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +1ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.841813Z","level":"INFO","fields":{"message":"SQL collation changed to windows-1252"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.841818Z","level":"INFO","fields":{"message":"Microsoft SQL Server\u0000\u0000 version 3892510736"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.841821Z","level":"INFO","fields":{"message":"Packet size change from '4096' to '4096'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.846526Z","level":"INFO","fields":{"message":"Begin transaction"},"target":"tiberius::tds::stream::token","span":{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"},"spans":[{"name":"DevDiagnostic"},{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"}]} +4ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.846554Z","level":"INFO","fields":{"message":"Rollback transaction"},"target":"tiberius::tds::stream::token","span":{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"},"spans":[{"name":"DevDiagnostic"},{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"}]} +0ms
  prisma:migrateEngine:stderr  {"timestamp":"2023-01-27T10:12:01.846566Z","level":"ERROR","fields":{"message":"The specified schema name \"myschema\" either does not exist or you do not have permission to use it.","code":2760},"target":"tiberius::tds::stream::token","span":{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"},"spans":[{"name":"DevDiagnostic"},{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"}]} +1ms
  prisma:migrateEngine:rpc  {
  jsonrpc: '2.0',
  error: {
    code: 4466,
    message: 'An error happened. Check the data field for details.',
    data: {
      is_panic: false,
      message: 'Migration `20230127101155_initial` failed to apply cleanly to the shadow database. \n' +
        'Error:\n' +
        'The specified schema name "myschema" either does not exist or you do not have permission to use it.\n' +
        '   0: migration_core::state::DevDiagnostic\n' +
        '             at migration-engine/core/src/state.rs:269',
      meta: [Object],
      error_code: 'P3006'
    }
  },
  id: 1
} +223ms
Error: Error: P3006

Migration `20230127101155_initial` failed to apply cleanly to the shadow database.
Error:
The specified schema name "myschema" either does not exist or you do not have permission to use it.
   0: migration_core::state::DevDiagnostic
             at migration-engine/core/src/state.rs:269

    at Object.<anonymous> (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:95044:25)
    at MigrateEngine.handleResponse (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:94897:36)
    at LineStream2.<anonymous> (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:94997:16)
    at LineStream2.emit (node:events:513:28)
    at addChunk (node:internal/streams/readable:315:12)
    at readableAddChunk (node:internal/streams/readable:289:9)
    at LineStream2.Readable.push (node:internal/streams/readable:228:10)
    at LineStream2._pushBuffer (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:94752:17)
    at LineStream2._transform (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:94746:8)
    at LineStream2.Transform._write (node:internal/streams/transform:205:23)
```