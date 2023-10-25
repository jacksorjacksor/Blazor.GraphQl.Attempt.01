Tutorial: https://www.aaron-powell.com/posts/2023-03-16-graphql-on-azure-part-14-using-dab-with-swa-and-blazor/

## Questions

- is 'data' the location that hold the DAB files?
- results in adding "dataApiLocation": "data" to `swa-cli.config.json`

- renamed `dab-config.json` to `staticwebapp.database.config.json`


[https://www.aaron-powell.com/posts/2023-03-16-graphql-on-azure-part-13-using-dab-with-swa-and-react/]
Notice the last line, "dataApiLocation": "data", this is the location of the folder that contains the schema.graphql and staticwebapp.database.config.json files which are going to be used by the Database Connections feature. Now, let’s start the SWA CLI:



## Error

```
[swa] ✖ Waiting for http://localhost:8000 to be ready
[swa] ✖ Could not connect to "http://localhost:8000". Is the server up and running?
[swa] node "C:\Users\jacks\AppData\Roaming\nvm\v18.18.2\node_modules\@azure\static-web-apps-cli\dist\msha\server.js" exited with code 0
--> Sending SIGTERM to other processes..
[run] cd "D:\Coding\dab\EIT\Blazor.GraphQl.Attempt.01\frontend" && dotnet watch run exited with code 1
--> Sending SIGTERM to other processes..
[dataApi] cd "D:\Coding\dab\EIT\Blazor.GraphQl.Attempt.01\data" && "C:\Users\jacks\.swa\dataApiBuilder\0.8.52\Microsoft.DataApiBuilder.exe" start -c staticwebapp.database.config.json --no-https-redirect exited with code 1
✖ SWA emulator stoped because Data API server exited with code 1.

```

This is using the CLI commands

## Variables

- Connection string
AccountEndpoint=https://localhost:8081/;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

- DB
SampleDB

- Container
Persons

## CLI commands
### Generate dab-config.json
dab init --database-type "cosmosdb_nosql" --graphql-schema schema.gql --cosmosdb_nosql-database SampleDB --connection-string "AccountEndpoint=https://localhost:8081/;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==" --host-mode "Development"

### Add entities to dab-config.json
dab add Person --source Persons --permissions "anonymous:*"

### Run DAB
dab start

### Query
{
    people {
      items{
        firstname
        Age
      }
    }
}