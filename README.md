# DVLD – Driving & Vehicle License Department

A Windows desktop system for managing driving licenses from the first application to issuing, renewing, replacing and detaining a license. Built with **C#**, **Windows Forms** and **SQL Server** on a **three-tier architecture**.

> Team project by [Khalil I. Al-Absi](https://github.com/kh-ibrahim4) and [Kareem Jehad](https://github.com/kareemjehad6).

## Features

### Licensing services
- **New local driving license** – application per license class, with fees and status tracking (new, cancelled, completed).
- **Test workflow** – vision, written and street tests taken in order; appointments can be scheduled, retaken and recorded with a pass or fail result and the number of trials.
- **First-time license issue** once all three tests are passed.
- **International license** issued from a valid local license.
- **Renew** an expired license.
- **Replace** a lost or damaged license.
- **Detain** a license with a fine, and **release** it once the fine is paid.
- **License history** for every person, local and international.

### Management
- **People** – add, edit, find and view people, with a personal photo and country.
- **Drivers** – list of everyone who holds a license.
- **Users** – system accounts with add, edit, change password and activation status.
- **Application types and test types** – editable titles and fees.

### Application
- Login screen with a "remember me" option.
- Lists with filtering on every management screen.
- Reusable user controls (person card, license card, application info) shared across forms.

## Architecture

The solution is split into three projects, each depending only on the one below it:

```
DVLD (Presentation)  ──►  DVLD_Buisness (Business logic)  ──►  DVLD_DataAccess (Data access)  ──►  SQL Server
```

| Project | Responsibility |
|---|---|
| `DVLD` | Windows Forms UI: forms, user controls, validation and formatting helpers |
| `DVLD_Buisness` | Business entities and rules (`clsPerson`, `clsLicense`, `clsTest`, `clsApplication`, ...) |
| `DVLD_DataAccess` | ADO.NET data access with parameterised `SqlCommand` queries |

## Tech stack

| Layer | Technology |
|---|---|
| Language | C# |
| Framework | .NET Framework 4.8, Windows Forms |
| Database | Microsoft SQL Server, ADO.NET |
| IDE | Visual Studio |

## Project structure

```
├── DVLD/                     # Presentation layer (startup project, contains DVLD.sln)
│   ├── Applications/         # Local, international, renew, replace, release
│   ├── Licenses/             # Issue, detain, license info and history
│   ├── Tests/                # Appointments, schedule and take test
│   ├── People/  Drivers/  User/  Login/
│   ├── Global Classes/       # Validation, formatting, current-user helpers
│   └── Resources/            # Icons and images
├── DVLD_Buisness/            # Business layer
└── DVLD_DataAccess/          # Data access layer
```

## Getting started

### Requirements

- Windows with Visual Studio 2019 or later (".NET desktop development" workload)
- .NET Framework 4.8
- Microsoft SQL Server

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/kh-ibrahim4/dvld-license-management.git
   ```
2. Create a SQL Server database named `DVLD`.

   > The database backup is not included in this repository. The application expects these tables: `People`, `Users`, `Countries`, `Applications`, `ApplicationTypes`, `LocalDrivingLicenseApplications`, `LicenseClasses`, `Licenses`, `InternationalLicenses`, `DetainedLicenses`, `Drivers`, `Tests`, `TestTypes`, `TestAppointments`, plus the list views used by the grids.
3. Set your own connection string in `DVLD_DataAccess/clsDataAccessSettings.cs`:
   ```csharp
   public static string ConnectionString = "Server=.;Database=DVLD;User Id=sa;Password=YOUR_PASSWORD;";
   ```
4. Open `DVLD/DVLD.sln` in Visual Studio, set `DVLD` as the startup project and run.

## Known limitations

- The database script is not part of the repository yet, so the app cannot run without recreating the schema.
- User passwords are stored and compared as plain text.
- "Remember me" saves the credentials in a plain text file next to the executable.
- The connection string is hard-coded instead of being read from a configuration file.

## Possible improvements

- Add the database creation script or a backup file.
- Hash passwords and store remembered credentials securely.
- Move the connection string to `App.config`.
- Add logging for database errors.

## Contributors

- **Khalil I. Al-Absi** – [GitHub](https://github.com/kh-ibrahim4) · [LinkedIn](https://www.linkedin.com/in/khalil-alabsi/)
- **Kareem Jehad** – [GitHub](https://github.com/kareemjehad6)
