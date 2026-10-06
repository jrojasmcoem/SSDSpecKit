# ContosoDashboard

The ContosoDashboard application is intended for TRAINING PURPOSES ONLY.

The ContosoDashboard repository contains the starter code project for training that teaches Spec-Driven Development (SDD) using the GitHub Spec Kit. ContosoDashboard is a fictional application created solely for educational purposes.

- The project codebase is NOT intended for use in production environments.
- The project architecture is NOT intended as a model for production applications.
- The project is NOT actively maintained and may contain bugs or security vulnerabilities.
- The project is provided "as-is" without warranties or support of any kind.
- The project implements mock authentication and authorization for training purposes only.
- The project does NOT implement cloud integration or external service dependencies (local only and offline to maximize training availability).
- The project demonstrates good coding practices, simplified for a training context, with known and documented limitations.

## Desarrollo guiado por especificaciones (Spec Kit / SDD)

Este repositorio ya incluye [GitHub Spec Kit](https://github.com/github/spec-kit).
Se conserva y documenta la instalación existente para empezar a mejorar el proyecto
sin reinicializarlo ni sobrescribir sus especificaciones. Spec Kit es una herramienta
de desarrollo, no una dependencia de la aplicación.

### Configuración incluida

La opción predeterminada es **GitHub Copilot en VS Code, con comandos `/speckit.*`
y scripts PowerShell**. PowerShell 7 permite usar los mismos scripts en Windows,
Linux y macOS; no se añade un segundo conjunto de scripts Bash ni extensiones opcionales.

| Ubicación | Propósito |
|-----------|-----------|
| `.github/prompts/` | Entradas de los comandos `/speckit.*` de Copilot Chat. |
| `.github/agents/` | Agentes de Spec Kit a los que delegan esos comandos. |
| `.github/copilot-instructions.md` | Instrucciones del repositorio, incluido el idioma español. |
| `.specify/memory/constitution.md` | Principios y puertas de calidad de ContosoDashboard. |
| `.specify/templates/` | Plantillas en español para especificación, plan, tareas, checklists, constitución y contexto del agente. |
| `.specify/scripts/powershell/` | Creación de funcionalidades, comprobación de prerrequisitos, preparación del plan y tareas y actualización del contexto. |
| `.specify/init-options.json`, `.specify/integration.json`, `.specify/integrations/` | Opciones y manifiestos de la instalación existente (`1.0.14.dev0`, integración `copilot`, scripts `ps`, numeración secuencial). |
| `.specify/workflows/` | Definición del ciclo SDD de Spec Kit; no es un workflow de GitHub Actions. |
| `.vscode/settings.json` | Recomendaciones de los comandos del flujo y sus revisiones. |
| `specs/` | Artefactos versionados de cada funcionalidad. |

Ya existe `specs/001-document-upload-management/spec.md`, en estado **Borrador**,
con su checklist de requisitos. Es una propuesta, no una garantía de implementación.
El código actual es ContosoDashboard: el contexto de negocio sobre clientes, ERP,
CSP-Tenant y pedidos no debe tratarse como funcionalidad implementada. Para incorporarlo,
crea una nueva especificación y valida su alcance y compatibilidad con la constitución.

### Requisitos locales

- **Git**, **PowerShell 7+** (`pwsh`) y **VS Code con GitHub Copilot** habilitado
  para tu cuenta. Abre la raíz del repositorio como carpeta de trabajo y usa Copilot Chat.
- Para trabajar con los archivos y scripts incluidos **no hace falta instalar Specify CLI**.
  El asistente de IA puede requerir conexión a Internet, aunque la aplicación sea local.
- Para compilar o ejecutar ContosoDashboard necesitas los requisitos de la aplicación:
  el SDK compatible con `ContosoDashboard/ContosoDashboard.csproj` (actualmente **.NET 10**)
  y SQL Server LocalDB para ejecutarla. No son requisitos para redactar especificaciones.

Desde la raíz, puedes comprobar PowerShell y consultar los scripts sin crear archivos:

```powershell
pwsh --version
git --version
pwsh -NoProfile -File .specify/scripts/powershell/create-new-feature.ps1 -Help
pwsh -NoProfile -File .specify/scripts/powershell/check-prerequisites.ps1 -Help
```

### Crear una funcionalidad

Parte de `main` actualizado y con el árbol de trabajo limpio. Ejecuta los siguientes
comandos **en Copilot Chat, uno por uno**, revisando cada resultado antes de continuar;
no son comandos de terminal:

```text
/speckit.specify Permitir filtrar las tareas por prioridad, conservando los permisos existentes.
/speckit.clarify
/speckit.plan Integrar la mejora en ContosoDashboard con Blazor Server y los servicios existentes, sin nuevas dependencias salvo justificación.
/speckit.tasks
/speckit.analyze
/speckit.implement
/speckit.converge
```

1. Revisa primero `.specify/memory/constitution.md`. Usa `/speckit.constitution`
   únicamente para acordar cambios en los principios, no para regenerarlos en cada iteración.
2. `/speckit.specify` crea una rama `NNN-nombre` y `specs/NNN-nombre/spec.md`.
   La numeración es secuencial; `001` ya está utilizado. Describe **qué** necesitas
   y **por qué**, con escenarios de aceptación y criterios medibles.
3. `/speckit.clarify` resuelve ambigüedades antes del diseño. No inventes reglas:
   conserva `[NEEDS CLARIFICATION: ...]` hasta acordarlas.
4. `/speckit.plan` prepara `plan.md` y los artefactos de diseño que correspondan
   (`research.md`, `data-model.md`, `quickstart.md`, `contracts/`).
5. `/speckit.tasks` genera `tasks.md`; `/speckit.analyze` revisa la consistencia
   entre especificación, plan y tareas antes de implementar. `/speckit.checklist`
   permite añadir una revisión de calidad de requisitos cuando sea útil.
6. `/speckit.implement` ejecuta las tareas. Valida los escenarios de aceptación,
   compila la aplicación si cambió código y ejecuta las pruebas disponibles.
   `/speckit.converge` identifica trabajo pendiente; repite implementación y
   convergencia hasta completarlo, revisando los cambios.
7. Incluye código y artefactos SDD en una PR hacia `main`, con los resultados de
   validación. La instalación de Spec Kit no crea ni publica una PR automáticamente.

Redacta los artefactos en español, manteniendo nombres de código y tokens que leen los
scripts: `NEEDS CLARIFICATION`, `N/A`, `[P]`, `[US1]`, `T001`, `FR-001`, `SC-001`,
`CHK001`, `**Language/Version**:`, `**Primary Dependencies**:`, `**Storage**:` y
`**Project Type**:`.

### Actualizar una especificación existente

Para continuar una funcionalidad, cambia a su rama `NNN-nombre` y abre su carpeta
en `specs/`. Edita `spec.md` directamente o pide a Copilot que actualice **ese archivo**;
no uses una nueva ejecución de `/speckit.specify` para una corrección de la misma funcionalidad.
Actualiza también los escenarios y criterios afectados, revisa el plan y ajusta las tareas
sin perder su trazabilidad ni el registro de trabajo completado. Vuelve a ejecutar
`/speckit.analyze` antes de implementar. Si la mejora es independiente, crea otra funcionalidad.

Los scripts resuelven la carpeta a partir de la rama. Si trabajas desde una rama con
otro nombre, puedes seleccionar explícitamente una especificación en una sesión PowerShell:

```powershell
$env:SPECIFY_FEATURE = '001-document-upload-management'
pwsh -NoProfile -File .specify/scripts/powershell/check-prerequisites.ps1 -PathsOnly -Json
# Tras disponer de plan.md y tasks.md:
pwsh -NoProfile -File .specify/scripts/powershell/check-prerequisites.ps1 -Json -RequireTasks -IncludeTasks
Remove-Item Env:SPECIFY_FEATURE
```

`SPECIFY_FEATURE` debe coincidir con la carpeta elegida; no crea ni cambia ramas.
La variable se hereda por los procesos iniciados desde esa terminal, no por un VS Code
ya abierto. La comprobación de implementación falla intencionadamente si faltan
`plan.md` o `tasks.md`; el borrador `001` todavía no contiene esos archivos.

### Mantenimiento y solución de problemas

- Versiona `.specify/`, los comandos de Copilot y `specs/`; no versiones secretos,
  entornos locales ni artefactos de compilación. `.specify/.gitignore` ya excluye
  el selector local `feature.json` y las configuraciones locales de extensiones.
- Si no aparecen los comandos, comprueba que abriste la raíz, que Copilot está
  habilitado y que VS Code permite los archivos de prompts del workspace; recarga la ventana.
  Usa los comandos con punto (`/speckit.specify`) de esta instalación: otras versiones
  de Spec Kit pueden usar skills con guion (`/speckit-specify`).
- Si aparece «Not on a feature branch», usa la rama `NNN-nombre` correcta o
  `SPECIFY_FEATURE`. Si faltan artefactos, completa plan y tareas antes de implementar.
- No ejecutes `specify init --here --force` sobre esta instalación: podría reemplazar
  personalizaciones. Para una actualización deliberada, consulta la
  [guía oficial](https://github.com/github/spec-kit), elige una versión concreta,
  sigue sus requisitos de CLI (Python 3.11+ y `uv`), trabaja en una rama con los
  cambios previos guardados y revisa el diff antes de integrar. Conserva las
  traducciones, la constitución y las especificaciones. No se instala una CLI global
  ni se actualiza automáticamente la versión de Spec Kit en esta configuración.

## 🔒 Security Features (Training Implementation)

This application includes a **mock authentication system** designed for training without external dependencies:

- ✅ Cookie-based authentication (8-hour sliding expiration)
- ✅ Claims-based identity with user roles
- ✅ Razor Pages for login/logout (proper HTTP request handling)
- ✅ Custom authentication state provider for Blazor Server integration
- ✅ Authorization enforcement on all protected pages (`[Authorize]` attribute)
- ✅ Role-based access control (RBAC) with hierarchical permissions
- ✅ Service-level security to prevent unauthorized data access
- ✅ IDOR (Insecure Direct Object Reference) protection
- ✅ Defense in depth (middleware, page attributes, service checks)
- ✅ Security headers (CSP, X-Frame-Options, X-XSS-Protection, etc.)
- ✅ Cookie security with sliding expiration
- ✅ User isolation - each user sees only their authorized data
- ✅ No external services required (suitable for offline training)

**Note**: The mock authentication is suitable for training only. Production deployments require proper identity providers with password hashing, MFA, OAuth 2.0/OpenID Connect, and compliance with security standards (WCAG 2.1, TLS encryption, audit logging).

### Mock Login System

**Available Users** (no password required - select from dropdown):

| Display Name | Email | Role | Department |
|-------------|-------|------|------------|
| System Administrator | `admin@contoso.com` | Administrator | IT |
| Camille Nicole | `camille.nicole@contoso.com` | Project Manager | Engineering |
| Floris Kregel | `floris.kregel@contoso.com` | Team Lead | Engineering |
| Ni Kang | `ni.kang@contoso.com` | Employee | Engineering |

**Login Process:**

1. Navigate to `/login` (automatic redirect if not authenticated)
2. Select a user from the dropdown
3. Click "Login" - you'll be redirected to the dashboard as that user

⚠️ **Important:** This mock authentication system is for **training only**. Production applications should use Azure AD, Identity Server, Auth0, or similar identity providers with proper password hashing, MFA, and OAuth 2.0/OpenID Connect.

## Overview

ContosoDashboard is built using ASP.NET Core 8.0 with Blazor Server and provides a centralized platform for:

- Task management and tracking
- Project oversight and collaboration
- Team coordination
- Notifications and announcements
- User profile management

## Features

### ✅ Implemented Features

- **Mock Authentication System**: User selection login, cookie-based auth, claims-based identity
- **Authorization Enforcement**: `[Authorize]` attributes on all protected pages, role-based policies
- **Dashboard Home Page**: Personalized dashboard with summary cards showing active tasks, due dates, projects, and notifications
- **Task Management**: View, filter, sort, and update tasks with priority levels and status tracking
- **Project Management**: Browse projects with completion percentages, team members, and status indicators
- **Project Details**: Comprehensive project view with task list, team members, and project statistics
- **Team Directory**: Browse team members by department with status, roles, and contact information
- **Notifications Center**: View and manage all notifications with read/unread status and priority badges
- **User Profile**: Update personal information, availability status, and notification preferences
- **Service-Level Security**: Authorization checks prevent IDOR vulnerabilities
- **Data Models**: Complete entity framework models for Users, Tasks, Projects, Notifications, and Announcements
- **Business Services**: Service layer for all core functionality (Tasks, Projects, Users, Notifications, Dashboard)
- **Database Context**: EF Core DbContext with relationships, indexes, and seed data

### 🔧 Technical Stack

- **Framework**: ASP.NET Core 8.0
- **UI**: Blazor Server
- **Database**: SQL Server LocalDB with Entity Framework Core
- **Authentication**: Cookie-based mock authentication for training (Azure AD/Microsoft Entra ID ready)
- **Authorization**: Claims-based identity with role-based access control
- **Styling**: Bootstrap 5.3 with Bootstrap Icons
- **Architecture**: Clean separation of concerns with Models, Services, Data, and Pages layers
- **Security**: IDOR protection, service-level authorization, `[Authorize]` attributes

## Architecture Principles

### Offline-First with Cloud Migration Path

This training application follows an **offline-first architecture** with abstraction layers that enable seamless migration to Azure services:

**Current Implementation (Training/Offline):**
- **Database**: SQL Server LocalDB (offline development database)
- **File Storage**: Local filesystem for any file-based features
- **Authentication**: Cookie-based mock authentication

**Production Migration Path:**
- **Database**: Azure SQL Database (replace connection string, no code changes)
- **File Storage**: Azure Blob Storage (swap `IFileStorageService` implementation)
- **Authentication**: Microsoft Entra ID (replace authentication middleware)

**Key Design Pattern - Infrastructure Abstraction:**

All infrastructure dependencies use **interface abstractions** to enable switching between local and cloud implementations:

```csharp
// Example: File storage abstraction
public interface IFileStorageService
{
    Task<string> UploadAsync(Stream fileStream, string fileName, string contentType);
    Task DeleteAsync(string filePath);
    Task<Stream> DownloadAsync(string filePath);
}

// Training: LocalFileStorageService (uses System.IO)
// Production: AzureBlobStorageService (uses Azure SDK)
// Swap via dependency injection - no business logic changes required
```

**Benefits of This Approach:**
- Students learn proper abstraction patterns and dependency injection
- Training works offline without Azure subscriptions or cloud costs
- Migration to production requires only configuration and implementation swaps
- Business logic remains unchanged during cloud migration
- Demonstrates industry-standard separation of concerns

**File upload best practice:** When implementing file uploads, generate unique file paths (using GUID) before database insertion to prevent duplicate key violations and orphaned records.

## Getting Started

### Prerequisites

- .NET 8.0 SDK or later
- SQL Server LocalDB
- Visual Studio 2022 or Visual Studio Code

### Quick Start

1. **Navigate to the project directory**:

   ```powershell
   cd ContosoDashboard
   ```

2. **Run the application** (database will be created automatically):

   ```powershell
   dotnet run
   ```

3. **Open your browser** to `http://localhost:5000`

4. **Login** - Select any user from the dropdown (no password required)

The application automatically creates and seeds the database on first run with sample users, projects, tasks, and announcements.

### Testing Security Features

#### Test 1: Authentication Required

- Open browser in incognito mode
- Try to navigate to `https://localhost:xxxx/tasks`
- Expected: Redirect to `/login`

#### Test 2: User Isolation

- Login as "Ni Kang"
- Note the tasks and projects shown
- Logout and login as "Floris Kregel"
- Expected: Different tasks and projects displayed

#### Test 3: IDOR Protection

- Login as "Ni Kang" and view a project (note the ID in URL)
- Logout and login as "System Administrator"
- Try to access the same project by URL
- Expected: Access only if you're a member

#### Test 4: Role-Based Features

- Login as different users to see varying levels of access
- Employee: View assigned tasks, update status
- Project Manager: Manage projects, assign tasks
- Administrator: Full system access

## Project Structure

```plaintext
ContosoDashboard/
├── Data/
│   └── ApplicationDbContext.cs      # EF Core database context
├── Models/
│   ├── User.cs                      # User entity with roles
│   ├── TaskItem.cs                  # Task entity
│   ├── Project.cs                   # Project entity
│   ├── TaskComment.cs               # Task comments
│   ├── Notification.cs              # User notifications
│   ├── ProjectMember.cs             # Project team members
│   └── Announcement.cs              # System announcements
├── Services/
│   ├── IUserService.cs / UserService.cs
│   ├── ITaskService.cs / TaskService.cs
│   ├── IProjectService.cs / ProjectService.cs
│   ├── INotificationService.cs / NotificationService.cs
│   ├── IDashboardService.cs / DashboardService.cs
│   └── CustomAuthenticationStateProvider.cs  # Blazor Server auth integration
├── Pages/
│   ├── Index.razor                  # Dashboard home page
│   ├── Login.cshtml / Login.cshtml.cs  # Mock authentication login (Razor Page)
│   ├── Logout.cshtml / Logout.cshtml.cs  # Logout handler (Razor Page)
│   ├── Tasks.razor                  # Task list and management
│   ├── Projects.razor               # Project list view
│   ├── ProjectDetails.razor         # Individual project details
│   ├── Team.razor                   # Team member directory
│   ├── Notifications.razor          # Notification center
│   ├── Profile.razor                # User profile page
│   └── _Host.cshtml                 # Blazor Server host page
├── Shared/
│   ├── MainLayout.razor             # Main layout template
│   └── NavMenu.razor                # Navigation sidebar
├── wwwroot/
│   └── css/site.css                 # Custom styles
├── Program.cs                       # Application entry point
├── appsettings.json                 # Configuration
└── ContosoDashboard.csproj          # Project file
```

## Configuration

### Database Connection

The default connection string in `appsettings.json` uses SQL Server LocalDB:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoDashboard;Trusted_Connection=True;MultipleActiveResultSets=true"
}
```

Update this if using a different SQL Server instance.

### Production Authentication Guidance

This training application uses mock authentication. For production applications, you would need to:

- Implement proper identity providers (Azure AD, Identity Server, Auth0)
- Add password hashing and salting (e.g., bcrypt, PBKDF2)
- Enable multi-factor authentication (MFA)
- Implement OAuth 2.0/OpenID Connect protocols
- Add rate limiting and account lockout policies
- Implement comprehensive audit logging
- Use secure session management with idle timeouts
- Implement password complexity requirements and rotation policies

See [Microsoft's ASP.NET Core Security documentation](https://docs.microsoft.com/aspnet/core/security/) for production implementation guidance.

### User Roles

The application supports four role levels with hierarchical permissions:

- **Employee**: View and update assigned tasks, view projects where member, manage own profile
- **TeamLead**: All Employee permissions plus view team member activities
- **ProjectManager**: All TeamLead permissions plus create/manage projects, assign tasks
- **Administrator**: Full system access including all administrative functions

## Sample Data

The application includes pre-seeded data for testing:

**Users** (all available for mock login):

- `admin@contoso.com` - System Administrator (Administrator role)
- `camille.nicole@contoso.com` - Camille Nicole (Project Manager role)
- `floris.kregel@contoso.com` - Floris Kregel (Team Lead role)
- `ni.kang@contoso.com` - Ni Kang (Employee role)

**Project**:

- "ContosoDashboard Development" with 3 sample tasks in various states

## Application Pages

| Page | Route | Description | Auth Required |
|------|-------|-------------|---------------|
| Login | `/login` | User selection for mock auth | No |
| Dashboard | `/` | Summary, announcements, quick actions | Yes |
| Tasks | `/tasks` | View and manage your tasks | Yes |
| Projects | `/projects` | View your projects | Yes |
| Project Details | `/projects/{id}` | Detailed project view | Yes (member only) |
| Team | `/team` | View team members | Yes |
| Notifications | `/notifications` | Manage notifications | Yes |
| Profile | `/profile` | Edit your profile | Yes |
| Logout | `/logout` | End session and clear cookies | Yes |

## Key Functionalities

### Dashboard (Home Page)

- Summary cards with real-time metrics
- Active announcements display
- Quick action links
- Recent notifications feed

### Task Management

- Filter by status, priority, and project
- Quick status updates via dropdown
- Priority-based color coding
- Overdue task highlighting

### Project Management

- Project cards with progress bars
- Completion percentage calculation
- Team member visibility
- Status badges

### User Profile

- Profile information editing
- Availability status management
- Notification preferences
- Display initials when no photo is set

## Troubleshooting

### Can't Login

- Ensure database is created (run `dotnet run` to auto-create)
- Check that seeded users exist in database
- Clear browser cookies and try again

### Redirected to Login After Login

- Check browser cookies are enabled
- Clear browser cache and cookies
- Try incognito/private mode

### Can't Access a Page

- Verify you're logged in (user name shown in top-right)
- Check if your role has permission for that resource
- Verify you're a member of the project/task you're trying to access

### Database Issues

**Option 1: Recreate via LocalDB**

```powershell
sqllocaldb stop mssqllocaldb
sqllocaldb delete mssqllocaldb
# Then run the application - database will be recreated automatically
```

**Option 2: Using EF Tools**

- Delete database: `dotnet ef database drop --force`
- Recreate: Run application (auto-creates with seed data)

**Note**: The application uses `EnsureCreated()` for development, so just running `dotnet run` will automatically create and seed the database if it doesn't exist.

## Security Concepts and Patterns

This training application demonstrates the following security concepts and patterns:

1. **Authentication Patterns** - How to implement and configure authentication
2. **Authorization Enforcement** - Using attributes and policies
3. **Claims-Based Identity** - Working with user claims
4. **IDOR Prevention** - Service-level authorization checks
5. **Security Best Practices** - Defense in depth, least privilege
6. **ASP.NET Core Security** - Industry-standard patterns and middleware

## Known Limitations (Training Context)

This is a **training application**, not production code. Known limitations include:

- **Mock authentication**: No real passwords - anyone can select any user account
- **No rate limiting**: Vulnerable to brute force attacks and denial of service
- **No audit logging**: Security events (login, failed auth, data changes) are not logged
- **Simplified input validation**: Production apps need more comprehensive validation
- **No session timeout warnings**: Users aren't warned before session expiration
- **CSP includes unsafe directives**: `'unsafe-inline'` and `'unsafe-eval'` required for Blazor Server but not ideal for security
- **No email verification**: User emails are not validated
- **No account lockout**: Failed login attempts don't trigger account locks

These limitations are **intentional** for training purposes to keep the application simple and self-contained. Production applications must address all of these security concerns.

## Code Quality Features

The application demonstrates good coding practices:

- Database indexes on frequently queried fields for performance
- Async/await pattern throughout for non-blocking operations
- Entity Framework Core with eager loading (`.Include()`) to prevent N+1 query problems
- Clean separation of concerns (Models, Services, Data, Pages)
- Dependency injection for loose coupling and testability
