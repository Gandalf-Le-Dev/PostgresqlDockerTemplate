# Usage instructions

## .NET Core

### Connection string

The connection string can be set in the appsettings.json file. The default connection string is:

```json
"ConnectionStrings": {
	"DefaultConnection": "UserID=user;Password=password;Host=localhost;Port=5432;Database=name_db;"
  }
```

### Database

- Migrations can be created using the following command:

	```powershell
	dotnet ef migrations add Init [-s ..\BlazorSandbox\] 
	```

	> `-s` is optional and is used to specify the startup project. In the case where the data context is in a different project than the startup project, the `-s` parameter must be used. And this command must be executed in the project where the data context is located.

<br/>
<br/>

- The database can be created or migrated using the following commands:

	```powershell
	dotnet ef database update [-s ..\BlazorSandbox\]
	```

	> `-s` is optional and is used to specify the startup project. In the case where the data context is in a different project than the startup project, the `-s` parameter must be used. And this command must be executed in the project where the data context is located.
