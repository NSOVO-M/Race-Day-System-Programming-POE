#  RaceDay - Sports Event Management System

RaceDay is a full-stack, multi-project solution designed to manage sports events, participants, and organiser workflows. It features a robust RESTful API backend, a Model-View-Controller (MVC) frontend, and a comprehensive suite of unit tests.

##  Architecture & Technologies

This solution is built using **.NET 8** and follows a Clean Architecture approach, separated into three main projects:

1.  **`RaceDay.API`** (Backend)
    *   **Framework:** ASP.NET Core Web API
    *   **Database:** SQL Server (Entity Framework Core)
    *   **Authentication:** JWT (JSON Web Tokens) with Role-Based Access Control (Admin, Organiser, Participant).
    *   **Security:** Password hashing using `IPasswordHasher<User>`.
    *   **Storage:** Azure Blob Storage (Emulated locally via **Azurite** in Docker) for event banner images.
2.  **`RaceDay.MVC`** (Frontend)
    *   **Framework:** ASP.NET Core MVC
    *   **UI/UX:** Bootstrap 5 (Customized with modern gradient styling)
    *   **Communication:** `HttpClient` interacting with the API, passing JWT tokens via Session state.
    *   **Features:** Role-specific dashboards, event browsing, enrolment systems, and admin CRUD operations.
3.  **`RaceDay.Tests`** (Testing)
    *   **Framework:** xUnit & Moq
    *   **Purpose:** Unit testing API controllers (Auth, Events) using in-memory databases to ensure reliable, isolated tests.

##  Getting Started (Local Development)

### Prerequisites
*   [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
*   [Visual Studio 2022](https://visualstudio.microsoft.com/) (with ASP.NET and web development workload)
*   [Docker Desktop](https://www.docker.com/products/docker-desktop/) (For running the Azurite Storage Emulator)
*   SQL Server (LocalDB or Express)

### 1. Database Setup
1. Open the `appsettings.json` in `RaceDay.API` and ensure the `DefaultConnection` string points to your local SQL Server instance.
2. Open the **Package Manager Console** (Tools > NuGet Package Manager > Package Manager Console), set `RaceDay.API` as the default project, and run:
   ```powershell
   Update-Database
## Azure Blob Storage (Azurite) Setup
The API uses Azurite to emulate Azure Blob Storage locally for event banners.

Ensure Docker Desktop is running.

Start the Azurite container via the terminal or Visual Studio Connected Services:

bash
docker run -p 10000:10000 -p 10001:10001 -p 10002:10002 mcr.microsoft.com/azure-storage/azurite
The API is already configured to use UseDevelopmentStorage=true, so it will connect to this container automatically.

## Running Tests
The solution includes automated unit tests for the API controllers.

In Visual Studio, navigate to Test > Test Explorer.

Click Run All to execute the test suite.

Note: The CI/CD pipeline (GitHub Actions) is configured to automatically run these tests on every push to the main branch.
