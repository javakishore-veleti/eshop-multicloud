
```shell

dotnet new sln -n eshop-multicloud

mkdir src

# Core (Domain / Interfaces)
dotnet new classlib -n eShop.Core -o src/eShop.Core

# Infrastructure (EF Core, Redis, DAO)
dotnet new classlib -n eShop.Infrastructure -o src/eShop.Infrastructure

#Services (Business logic, cache-aside)
dotnet new classlib -n eShop.Services -o src/eShop.Services

# UI (Blazor – recommended)
dotnet new blazor -n eShop.Blazor -o src/eShop.Blazor
#You can replace Blazor with MVC later if you want:
dotnet new mvc -n eShop.Web -o src/eShop.Web

# Add Projects to the Solution
dotnet sln add src/eShop.Core/eShop.Core.csproj
dotnet sln add src/eShop.Infrastructure/eShop.Infrastructure.csproj
dotnet sln add src/eShop.Services/eShop.Services.csproj
dotnet sln add src/eShop.Blazor/eShop.Blazor.csproj

# Add Project References (Correct Dependency Flow)

# Infrastructure → Core
dotnet add src/eShop.Infrastructure reference src/eShop.Core

# Services → Core + Infrastructure
dotnet add src/eShop.Services reference src/eShop.Core
dotnet add src/eShop.Services reference src/eShop.Infrastructure

# UI → Core + Services
dotnet add src/eShop.Blazor reference src/eShop.Core
dotnet add src/eShop.Blazor reference src/eShop.Services

# Build & Run to Verify
dotnet build
dotnet run --project src/eShop.Blazor


```
