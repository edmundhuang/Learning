# Basic ID4 Server

### Create basic IdentityServer 
```
md quickstart
cd quickstart

md src
cd src

dotnet new is4empty -n IdentityServer
```

```
cd ..
dotnet new sln -n Quickstart
dotnet sln add ./src/IdentityServer/IdentityServer.csproj
```

Launchsetting.json
Change https to http
"applicationUrl": "http://localhost:5001"

### Run service
···
dotnet run
···
Navigate to http://localhost:5000/.well-known/openid-configuration


