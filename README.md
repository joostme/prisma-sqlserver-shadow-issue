# Prisma SQLServer Shadow DB issue

When running `prisma migrate dev` a second time after creating the initial migration, we get the following error:

```sh
Error: Error: P3006

Migration `20230818062215_initial` failed to apply cleanly to the shadow database.
Error:
The specified schema name "myschema" either does not exist or you do not have permission to use it.
   0: schema_core::state::DevDiagnostic
             at schema-engine/core/src/state.rs:270

    at Object.<anonymous> (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93540:25)
    at SchemaEngine.handleResponse (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93388:36)
    at LineStream2.<anonymous> (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93491:16)
    at LineStream2.emit (node:events:513:28)
    at addChunk (node:internal/streams/readable:315:12)
    at readableAddChunk (node:internal/streams/readable:289:9)
    at LineStream2.Readable.push (node:internal/streams/readable:228:10)
    at LineStream2._pushBuffer (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93167:17)
    at LineStream2._transform (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93161:8)
    at LineStream2.Transform._write (node:internal/streams/transform:205:23)
```

## Steps to reproduce
1. Run the db with `docker-compose up`
2. Run `npm run migrate:dev` to create the initial migration (which is successful)
3. Run `npm run migrate:dev` again resulting in the error mentioned above.


## Detailed error log

```sh
> prisma-sqlserver-shadow-issue@1.0.0 migrate:dev
> DEBUG="*" prisma migrate dev

  prisma:engines  binaries to download libquery-engine, schema-engine +0ms
  prisma:loadEnv  project root found at /Users/joost/git/holi/prisma-sqlserver-shadow-issue/package.json +0ms
  prisma:tryLoadEnv  Environment variables loaded from /Users/joost/git/holi/prisma-sqlserver-shadow-issue/.env +0ms
  prisma:getConfig  Using getConfig Wasm +0ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +1ms
  prisma:loadEnv  project root found at /Users/joost/git/holi/prisma-sqlserver-shadow-issue/package.json +4ms
  prisma:tryLoadEnv  Environment variables loaded from /Users/joost/git/holi/prisma-sqlserver-shadow-issue/.env +3ms
Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma
  prisma:getConfig  Using getConfig Wasm +4ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +0ms
Datasource "db": SQL Server database

  prisma:validate  Using validate Wasm +0ms
  prisma:getConfig  Using getConfig Wasm +1ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +0ms
  prisma:getConfig  Using getConfig Wasm +1ms
  prisma:getConfig  config data retrieved without errors in getConfig Wasm +1ms
  prisma:schemaEngine:rpc  starting Schema engine with binary: /Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/@prisma/engines/schema-engine-darwin-arm64 +0ms
  prisma:schemaEngine:rpc  SENDING RPC CALL {"id":1,"jsonrpc":"2.0","method":"devDiagnostic","params":{"migrationsDirectoryPath":"/Users/joost/git/holi/prisma-sqlserver-shadow-issue/prisma/migrations"}} +6ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.798824Z","level":"INFO","fields":{"message":"Starting schema engine RPC server","git_hash":"6a3747c37ff169c90047725a05a6ef02e32ac97e"},"target":"schema_engine"} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.805288Z","level":"INFO","fields":{"message":"Performing a TLS handshake"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +6ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.805304Z","level":"WARN","fields":{"message":"Trusting the server certificate without validation."},"target":"tiberius::client::tls_stream::opentls_tls_stream","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.81306Z","level":"INFO","fields":{"message":"TLS handshake successful"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +8ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.813088Z","level":"WARN","fields":{"message":"Turning TLS off after a login. All traffic from here on is not encrypted."},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.817396Z","level":"INFO","fields":{"message":"Database change from 'mydb' to 'master'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +4ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.817411Z","level":"INFO","fields":{"message":"Changed database context to 'mydb'."},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.817414Z","level":"INFO","fields":{"message":"SQL collation changed to windows-1252"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.817418Z","level":"INFO","fields":{"message":"Microsoft SQL Server\u0000\u0000 version 3490119695"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:22.817422Z","level":"INFO","fields":{"message":"Packet size change from '4096' to '4096'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.311564Z","level":"INFO","fields":{"message":"Performing a TLS handshake"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +495ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.311608Z","level":"WARN","fields":{"message":"Trusting the server certificate without validation."},"target":"tiberius::client::tls_stream::opentls_tls_stream","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +1ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.321683Z","level":"INFO","fields":{"message":"TLS handshake successful"},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +8ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.321716Z","level":"WARN","fields":{"message":"Turning TLS off after a login. All traffic from here on is not encrypted."},"target":"tiberius::client::connection","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.325521Z","level":"INFO","fields":{"message":"Database change from 'prisma_migrate_shadow_db_9bbe5b01-06d6-498b-a38e-3bec2b8c72f3' to 'master'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +4ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.325536Z","level":"INFO","fields":{"message":"Changed database context to 'prisma_migrate_shadow_db_9bbe5b01-06d6-498b-a38e-3bec2b8c72f3'."},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.325541Z","level":"INFO","fields":{"message":"SQL collation changed to windows-1252"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.325545Z","level":"INFO","fields":{"message":"Microsoft SQL Server\u0000\u0000 version 3490119695"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.325549Z","level":"INFO","fields":{"message":"Packet size change from '4096' to '4096'"},"target":"tiberius::tds::stream::token","span":{"name":"DevDiagnostic"},"spans":[{"name":"DevDiagnostic"}]} +0ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.33013Z","level":"INFO","fields":{"message":"Begin transaction"},"target":"tiberius::tds::stream::token","span":{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"},"spans":[{"name":"DevDiagnostic"},{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"}]} +5ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.330332Z","level":"INFO","fields":{"message":"Rollback transaction"},"target":"tiberius::tds::stream::token","span":{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"},"spans":[{"name":"DevDiagnostic"},{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"}]} +1ms
  prisma:schemaEngine:stderr  {"timestamp":"2023-08-18T06:22:23.330369Z","level":"ERROR","fields":{"message":"The specified schema name \"myschema\" either does not exist or you do not have permission to use it.","code":2760},"target":"tiberius::tds::stream::token","span":{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"},"spans":[{"name":"DevDiagnostic"},{"db.statement":"BEGIN TRY\n\nBEGIN TRAN;\n\n-- CreateTable\nCREATE TABLE [myschema].[User] (\n    [id] NVARCHAR(1000) NOT NULL,\n    [name] NVARCHAR(1000) NOT NULL,\n    [email] NVARCHAR(1000) NOT NULL,\n    [balance] FLOAT(53) NOT NULL CONSTRAINT [User_balance_df] DEFAULT 0,\n    CONSTRAINT [User_pkey] PRIMARY KEY CLUSTERED ([id])\n);\n\nCOMMIT TRAN;\n\nEND TRY\nBEGIN CATCH\n\nIF @@TRANCOUNT > 0\nBEGIN\n    ROLLBACK TRAN;\nEND;\nTHROW\n\nEND CATCH\n","name":"quaint:query"}]} +2ms
  prisma:schemaEngine:rpc  {
  jsonrpc: '2.0',
  error: {
    code: 4466,
    message: 'An error happened. Check the data field for details.',
    data: {
      is_panic: false,
      message: 'Migration `20230818062215_initial` failed to apply cleanly to the shadow database. \n' +
        'Error:\n' +
        'The specified schema name "myschema" either does not exist or you do not have permission to use it.\n' +
        '   0: schema_core::state::DevDiagnostic\n' +
        '             at schema-engine/core/src/state.rs:270',
      meta: [Object],
      error_code: 'P3006'
    }
  },
  id: 1
} +614ms
Error: Error: P3006

Migration `20230818062215_initial` failed to apply cleanly to the shadow database.
Error:
The specified schema name "myschema" either does not exist or you do not have permission to use it.
   0: schema_core::state::DevDiagnostic
             at schema-engine/core/src/state.rs:270

    at Object.<anonymous> (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93540:25)
    at SchemaEngine.handleResponse (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93388:36)
    at LineStream2.<anonymous> (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93491:16)
    at LineStream2.emit (node:events:513:28)
    at addChunk (node:internal/streams/readable:315:12)
    at readableAddChunk (node:internal/streams/readable:289:9)
    at LineStream2.Readable.push (node:internal/streams/readable:228:10)
    at LineStream2._pushBuffer (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93167:17)
    at LineStream2._transform (/Users/joost/git/holi/prisma-sqlserver-shadow-issue/node_modules/prisma/build/index.js:93161:8)
    at LineStream2.Transform._write (node:internal/streams/transform:205:23)
```