# Usage instructions

## Start and Stop Docker Compose
You can start the docker compose with the `start_db_container.bat` script. This script checks whether the Docker container `postgres_db` is already running. If it's not running, the script starts the Docker Compose services in detached mode. If the container is already running, it informs the user. This ensures that the PostgreSQL database service managed by Docker Compose is running before proceeding with further operations.

pgAdmin will be accessible at [http://localhost:5050](http://localhost:5050/)

You can also stop the docker compose with the `stop_db_container.bat` script. This script checks if the Docker container 'postgres_db' is currently running. If the container is not running, it notifies the user. If it is running, the script proceeds to stop the Docker Compose services, ensuring that the PostgreSQL database service managed by Docker Compose is properly shut down before any further actions

## Configure PGAdmin - [Official documentation](https://www.pgadmin.org/docs/pgadmin4/8.0/index.html)

You can set your pgAdmin default email and password in the `docker-compose.yml` in the services/pgadmin/environment section.

In the `servers.json` file you can configure your pgAdmin server. See official pgAdmin documentation about Servers for more information: [Import/Export Servers](https://www.pgadmin.org/docs/pgadmin4/latest/import_export_servers.html#json-format)

## Configure PostgreSQL - [Official documentation]()

You can set the default postgres database user, password and name in the `docker-compose.yml` in the services/postgres_db/environment section.

The file `pgpass` is used to automate the process of password authentication. See official documentation for more information: [The Password File](https://www.postgresql.org/docs/current/libpq-pgpass.html)

*Optional*: You can also load a schema.sql or any other script by adding this line in the services/postgres_db/volumes section: `- [location of the schema.sql file]:/docker-entrypoint-initdb.d/schema.sql`. See official documentation for more details: [PostgreSQL Docker image documentation](https://hub.docker.com/_/postgres#Initialization%20scripts:~:text=and%20POSTGRES_DB.-,Initialization%20scripts,-If%20you%20would)

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

## FAQ

**Q: My PotgreSQL container is rebooting and nerver starts.**

**A:** Make sure your `postgres_db_data/` folder is empty or contains working postgresql db files.
