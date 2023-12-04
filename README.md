# Usage instructions

## Start and Stop Docker Compose

- To start Docker Compose, use the `start_db_container.bat` script. This script checks whether the Docker container postgres_db is already running. If it's not, the script starts the Docker Compose services in detached mode. If the container is already running, it informs the user. This ensures that the PostgreSQL database service managed by Docker Compose is running before proceeding with further operations.

- PgAdmin will be accessible at [http://localhost:5050](http://localhost:5050/)

- To stop Docker Compose, use the `stop_db_container.bat` script. This script checks if the Docker container postgres_db is currently running. If the container is not running, it notifies the user. If it is running, the script proceeds to stop the Docker Compose services, ensuring that the PostgreSQL database service managed by Docker Compose is properly shut down before any further actions.

## Configure PGAdmin - [Official documentation](https://www.pgadmin.org/docs/pgadmin4/8.0/index.html)

- Set your PgAdmin default email and password in the `docker-compose.yml` file, under the `services/pgadmin/environment` section.

- In the `servers.json` file, you can configure your PgAdmin server. For more information, see the official PgAdmin documentation on [Import/Export Servers](https://www.pgadmin.org/docs/pgadmin4/latest/import_export_servers.html#json-format)

## Configure PostgreSQL - [Official documentation]()

- Set the default PostgreSQL database user, password, and name in the `docker-compose.yml` file, under the `services/postgres_db/environment` section.

- The `pgpass` file is used to automate the process of password authentication. For more information, see the [official documentation:The Password File](https://www.postgresql.org/docs/current/libpq-pgpass.html)

*Optional*: Load a `schema.sql` or any other script by adding the following line in the `services/postgres_db/volumes` section of `docker-compose.yml`: `- [location of the schema.sql file]:/docker-entrypoint-initdb.d/schema.sql`. For more details, see the [PostgreSQL Docker image documentation](https://hub.docker.com/_/postgres#Initialization%20scripts:~:text=and%20POSTGRES_DB.-,Initialization%20scripts,-If%20you%20would)

## .NET Core

### Connection string

Set the connection string in the `appsettings.json` file. The default connection string is:

```json
"ConnectionStrings": {
	"DefaultConnection": "UserID=user;Password=password;Host=localhost;Port=5432;Database=name_db;"
  }
```

### Database

- Create migrations using the following command:

	```powershell
	dotnet ef migrations add Init [-s ..\BlazorSandbox\] 
	```

	> The `-s` parameter is optional and specifies the startup project. If the data context is in a different project than the startup project, use the `-s` parameter. This command must be executed in the project where the data context is located.

<br/>
<br/>

- Create or migrate the database using the following commands:

	```powershell
	dotnet ef database update [-s ..\BlazorSandbox\]
	```

	> The `-s` parameter is optional and specifies the startup project. If the data context is in a different project than the startup project, use the `-s` parameter. This command must be executed in the project where the data context is located.

## FAQ

**Q: My PotgreSQL container is rebooting and nerver starts.**

**A:** Ensure your `postgres_db_data/` folder is empty or contains working PostgreSQL database files.
