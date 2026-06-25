# Backend Setup Guide - ASP.NET Core 8.0 with PostgreSQL

## Prerequisites
- .NET 8.0 SDK (Download from https://dotnet.microsoft.com/download/dotnet/8.0)
- PostgreSQL 13+ (Download from https://www.postgresql.org/download/)
- Visual Studio 2022 Community or VS Code
- Git

## Step 1: Create Project Structure

```bash
# Create solution
dotnet new globaljson --sdk-version 8.0.0 --roll-forward latestFeature
dotnet new sln -n HinduCalendar

# Create projects
dotnet new webapi -n HinduCalendar.API
dotnet new classlib -n HinduCalendar.Core
dotnet new classlib -n HinduCalendar.Infrastructure

# Add to solution
dotnet sln add HinduCalendar.API/HinduCalendar.API.csproj
dotnet sln add HinduCalendar.Core/HinduCalendar.Core.csproj
dotnet sln add HinduCalendar.Infrastructure/HinduCalendar.Infrastructure.csproj
```

## Step 2: Add NuGet Packages

```bash
# API Project
cd HinduCalendar.API
dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet add package AutoMapper.Extensions.Microsoft.DependencyInjection
dotnet add package Microsoft.EntityFrameworkCore.Npgsql

# Infrastructure Project
cd ../HinduCalendar.Infrastructure
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.Npgsql
dotnet add package Microsoft.EntityFrameworkCore.Tools
```

## Step 3: Database Setup

### PostgreSQL Connection
1. Open pgAdmin or psql
2. Create database:
   ```sql
   CREATE DATABASE hindu_calendar_db;
   CREATE DATABASE hindu_calendar_test_db;
   ```

### Update Connection String
Edit `HinduCalendar.API/appsettings.json`:
```json
"ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=hindu_calendar_db;Username=postgres;Password=your_password"
}
```

## Step 4: Create Entity Models

See files:
- `backend/HinduCalendar.Core/Entities/User.cs`
- `backend/HinduCalendar.Core/Entities/Festival.cs`
- `backend/HinduCalendar.Core/Entities/Event.cs`
- `backend/HinduCalendar.Core/Entities/PanchangData.cs`

## Step 5: Setup Database Context

Create `HinduCalendar.Infrastructure/Data/HinduCalendarContext.cs` (see provided file)

## Step 6: Run Migrations

```bash
# From project root
cd HinduCalendar.API

# Create initial migration
dotnet ef migrations add InitialCreate --project ../HinduCalendar.Infrastructure

# Update database
dotnet ef database update --project ../HinduCalendar.Infrastructure
```

## Step 7: Configure API Program.cs

See `HinduCalendar.API/Program.cs` for full configuration including:
- Authentication (JWT)
- CORS
- Entity Framework
- Dependency Injection
- AutoMapper

## Step 8: Run the API

```bash
cd HinduCalendar.API
dotnet run
```

API will be available at:
- http://localhost:5000
- https://localhost:5001
- Swagger UI: https://localhost:5001/swagger/index.html

## Step 9: Create Controllers

Create the following controllers:
- `AuthController` - Login, Register, Refresh Token
- `CalendarController` - Get calendar data, festivals, panchang
- `EventController` - CRUD operations for user events
- `AdminController` - Festival management (admin only)

## Database Schema Overview

### Users Table
- Id (PK)
- Username (Unique)
- Email (Unique)
- PasswordHash
- FirstName, LastName
- PreferredLanguage (hi, te, ta, kn, ml)
- Role (User, Admin)
- IsActive
- CreatedAt, UpdatedAt

### Festivals Table
- Id (PK)
- Name + Translations (NameHi, NameTe, NameTa, NameKn, NameMl)
- Description + Translations
- CelebrationDate
- CalendarType (lunar, solar, gregorian)
- LunarMonth, LunarDay
- IsImportant
- ImageUrl
- CreatedAt, UpdatedAt

### Events Table
- Id (PK)
- UserId (FK)
- Title, Description
- StartDate, EndDate
- Category
- ReminderEnabled
- ReminderMinutesBefore
- Notes
- CreatedAt, UpdatedAt

### PanchangData Table
- Id (PK)
- Date (Unique)
- Tithi, Nakshatra, Yoga, Karana
- Vaar (Day of week)
- RahuKalam, YamagandaTime, GulikaiKalam
- IsAuspicious
- Notes
- CreatedAt, UpdatedAt

## Troubleshooting

### Connection String Issues
- Verify PostgreSQL is running
- Check database name matches
- Verify credentials

### Migration Issues
```bash
# Remove last migration
dotnet ef migrations remove

# List migrations
dotnet ef migrations list
```

### Port Already in Use
```bash
# Specify different port
dotnet run --urls "https://localhost:5002"
```

## Next Steps
1. Create authentication services
2. Implement API controllers
3. Add business logic services
4. Set up error handling middleware
5. Add logging and monitoring
