# Inventory Management REST Service Using ASP.NET Core with JWT Token Authentication

## Overview

This sample shows how to build a JWT-secured inventory REST service with ASP.NET Core 3.1, Entity Framework Core, and SQL Server. The service issues a signed JSON Web Token from a dedicated token endpoint and uses that token to authorize CRUD operations on a product catalog exposed over HTTP, demonstrating a practical pattern for creating and protecting REST APIs with bearer authentication and server-side data access.

## Key Features

- Issues a signed JSON Web Token through the dedicated token API endpoint `POST api/token` so clients can authenticate once and reuse the token in subsequent requests.
- Secures the product catalog with bearer-token authorization applied to the products API controller, so unauthenticated requests are rejected.
- Provides full create, read, update, and delete operations for product records through standard REST actions exposed at the product API route `api/products`.
- Supports filtering and paging of the product list using the query parameters `inStock` (filter by availability), `skip` (rows to skip), and `take` (rows to return), so clients can page through inventory by availability and range.
- Persists product and user data in SQL Server through an Entity Framework Core database context with connection pooling for efficient, reusable database connections.
- Centralizes service registration and middleware configuration for authentication, authorization, routing, and controllers in the application startup so the request pipeline is configured in one place.

## Prerequisites

- Visual Studio 2022 or Visual Studio Code
- .NET SDK compatible with the project's target framework
- SQL Server 2017 or later / SQL Server Express / SQL Server LocalDB
- Postman or any HTTP client for testing the API

## How to Run the Project

### Visual Studio 2022

1. Clone or download this repository.
2. Open the solution file:

   `InventoryService/InventoryService.sln`

3. Update the SQL Server connection string under `ConnectionStrings:InventoryDatabase` in `InventoryService/appsettings.json` with the server name, database name, and authentication details for a database that you are authorized to access.
4. Update the JWT settings under `Jwt` in `InventoryService/appsettings.json` (`Key`, `Issuer`, `Audience`, `Subject`) with values suitable for your environment.
5. Restore the NuGet packages by rebuilding the solution.
6. Set the startup project to:

   `InventoryService`

7. Build the solution.
8. Run the application using `Ctrl+F5`.
9. Open the application URL displayed by Visual Studio after launch.
10. Verify that an unauthenticated request to `GET api/products` returns `401 Unauthorized` and that `POST api/token` with valid credentials returns a JWT that you can attach as a Bearer token to the `api/products` requests.

### Visual Studio Code

1. Clone or download this repository.
2. Open the repository folder in Visual Studio Code.
3. Open the integrated terminal.
4. Navigate to the project directory:

```bash
cd InventoryService
```

5. Update the SQL Server connection string under `ConnectionStrings:InventoryDatabase` in `InventoryService/appsettings.json` with the server name, database name, and authentication details for a database that you are authorized to access.
6. Update the JWT settings under `Jwt` in `InventoryService/appsettings.json` (`Key`, `Issuer`, `Audience`, `Subject`) with values suitable for your environment.
7. Restore the NuGet packages:

```bash
dotnet restore
```

8. Build the project:

```bash
dotnet build
```

9. Run the project:

```bash
dotnet run
```

10. Open the local URL displayed in the terminal after the application starts.
11. Verify that an unauthenticated request to `GET api/products` returns `401 Unauthorized` and that `POST api/token` with valid credentials returns a JWT that you can attach as a Bearer token to the `api/products` requests.

## Project Structure

- `InventoryService/Controllers/TokenController.cs` — issues a signed JWT in response to a valid user login request.
- `InventoryService/Controllers/ProductsController.cs` — exposes the authorized CRUD endpoints for the inventory catalog.
- `InventoryService/Models/Products.cs` — defines the product model stored in SQL Server.
- `InventoryService/Models/UserInfo.cs` — defines the user model used by the token endpoint.
- `InventoryService/Models/InventoryContext.cs` — defines the Entity Framework Core database context used to access products and users.

## Support and Feedback

- To report an issue specific to this sample, open a GitHub issue in this repository.
- Official documentation: [ASP.NET Core documentation](https://learn.microsoft.com/aspnet/core/)