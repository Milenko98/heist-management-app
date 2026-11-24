# Heist – Agency04 technical assignment

Full-stack application built in 2022 as a technical assignment during the hiring process at **Agency04**.
It manages heist members and their skills, plans heists with required skills, and tracks each heist through its lifecycle.

## Features

- **Members** – create members (name, sex, e-mail, main skill, status), view profiles, add, update and delete skills with levels.
- **Heists** – create heists with location and start/end time, define the required skills (skill, level, number of members).
- **Heist overview** – lists of all heists, heists that are ready to start and finished heists with outcomes.
- **REST API** documented with Swagger.

## Tech stack

| Layer    | Technologies |
|----------|--------------|
| Backend  | C#, ASP.NET Core Web API (.NET 6), Entity Framework Core 6, SQL Server, Swagger |
| Frontend | Angular 11, TypeScript, Angular Material, RxJS |

## Architecture

```
Agency04/
├── HeistWebApi/      # ASP.NET Core Web API – controllers, CORS, Swagger, DB setup
└── HeistService/     # business logic – services, interfaces, EF Core models, DTOs, DbContext
AngularFrontend/
└── Agency04/         # Angular SPA – components per screen, HTTP service
```

The API is split into a thin controller layer (`HeistController`, `HeistMemberController`) and a service layer (`HeistsService`, `HeistMemberService`). DTOs separate the API contract from the EF Core entities.

### Main endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/HeistMember/member` | Create a member |
| `GET` | `/api/HeistMember/members` | List members |
| `GET` / `PUT` | `/api/HeistMember/member/{id}/skills` | Get / update a member's skills |
| `DELETE` | `/api/HeistMember/member/{id}/skills/{name}` | Remove a member's skill |
| `POST` | `/api/Heist/heist` | Create a heist |
| `GET` | `/api/Heist/heists` | List heists |
| `GET` / `PATCH` | `/api/Heist/heist/{id}/skills` | Get / update required skills |

## Running locally

**Backend**

1. Open `Agency04/Agency04.sln` in Visual Studio 2022 (or use the .NET 6 SDK).
2. Set `ConnectionStrings:DefaultConnection` in `HeistWebApi/appsettings.json` to your SQL Server instance.
3. Run `HeistWebApi` – the database is created automatically on first start; Swagger UI is available at `/swagger`.

**Frontend**

```bash
cd AngularFrontend/Agency04
npm install
npx ng serve      # http://localhost:4200
```
