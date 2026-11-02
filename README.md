TestService .NET 9 SQL-enabled sample solution
---------------------------------------------

Projects:
- TestService.Domain
- TestService.Application
- TestService.Infrastructure (persistence + external)
- TestService.API
- TestService.UnitTests

Features included:
- Result pattern with ResultType in Application layer
- Sample Order and OrderItem domain entities
- GetOrderById CQRS query + handler (returns Result<OrderDto>)
- AutoMapper mapping profile
- EF Core DbContext with InMemory or SQL Server option
- Serilog basic setup (reads from configuration)
- SQL scripts to create tables and seed data (sql/ folder)
- Unit tests using xUnit + Moq

How to run with InMemory (development):
1. Ensure .NET 9 SDK is installed.
2. Open solution and run TestService.API (uses InMemory by default via appsettings.Development.json).

How to run with SQL Server (production):
1. Update appsettings.Production.json connection string (ConnectionStrings: DefaultConnection) with your SQL Server info.
2. Create the database and run the SQL scripts in /sql (or run EF Core migrations):
   - Use the provided SQL scripts: sql/001_create_tables.sql and sql/002_seed_data.sql
   - OR run EF Core migrations (recommended):
     dotnet tool install --global dotnet-ef --version 8.0.11
     dotnet ef migrations add InitialCreate --project src/Infrastructure/TestService.Infrastructure.csproj --startup-project src/API/TestService.API.csproj -o Persistence/Migrations
     dotnet ef database update --project src/Infrastructure/TestService.Infrastructure.csproj --startup-project src/API/TestService.API.csproj

Unit tests:
- Run `dotnet test` from solution root.
