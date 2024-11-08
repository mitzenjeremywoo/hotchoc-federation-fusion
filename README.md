product

dotnet fusion subgraph config set http --url http://localhost:5051

please remember to edit and update your schema name subgraph-config.json

{"subgraph":"accounts","http":{"baseAddress":"http://localhost:5054/"}}

before trying to export and compose it

dotnet run -- schema export --output schema.graphql

dotnet fusion subgraph pack

dotnet fusion compose -p .\gateway\gateway.zip -s .\accounts\

inventory

dotnet fusion subgraph config set http --url http://localhost:5052

please remember to edit and update your schema name subgraph-config.json

{"subgraph":"inventory","http":{"baseAddress":"http://localhost:5054/"}}

before trying to export and compose it

dotnet run -- schema export --output schema.graphql

dotnet fusion subgraph pack

dotnet fusion compose -p .\gateway\gateway.zip -s .\Inventory\

products

dotnet fusion subgraph config set http --url http://localhost:5053

dotnet run -- schema export --output schema.graphql

dotnet fusion subgraph pack

dotnet fusion compose -p .\gateway\gateway.zip -s .\products\

reviews dotnet fusion subgraph config set http --url http://localhost:5054

dotnet run -- schema export --output schema.graphql

dotnet fusion subgraph pack

dotnet fusion compose -p .\gateway\gateway.zip -s .\reviews\

please remember to edit and update your schema name subgraph-config.json st {"subgraph":"reviews","http":{"baseAddress":"http://localhost:5054/"}}

tye

--- account level-- services.AddSingleton(ConnectionMultiplexer.Connect("localhst:7000"))

services.AddSingleton(). AddGraphqlServer() .AddQueryType() .InitializeOnStartup() .PublishSchemaDefinition( c => c.SetName("accounts") .IgnoreRootTypes .AddTypeExtensionFromFile("stitching") .PublishToRedis("Demo", sp => sp.GetRequiredService)

)

Gateway level

services.AddSingleton(). AddGraphqlServer() .AddQueryType(d => d.Name("Query")) .InitializeOnStartup() .AddRemoteSchemaFromRedis("Demo", sp => sp.GetRequiredService)