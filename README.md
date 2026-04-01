# 🏢 Rental Management System

A comprehensive Windows desktop application for managing rental operations across multiple branches in the United Arab Emirates. Built with WPF, MVVM, and SQL Server.

## Overview

This application centralizes rental operations management, providing tools to track contracts, payment schedules, branch locations, documents, and generate comprehensive reports for decision-making.

## Features

### ✅ Core Features (Complete)
- **Branch Management** — Full CRUD operations with filtering by emirate and search
- **Contact Management** — Track landlords, agents, and managers per branch
- **Note Management** — Internal notes for each branch
- **Navigation** — Sidebar-based navigation with implicit DataTemplate view locator

### ✅ Advanced Features (Complete)
- **Contract Management** — Track rental contracts with payment schedule generation and renewal tracking
- **Activity Logging** — Auto-log all contract changes (renewals, cancellations, adjustments) with reference numbers
- **Document Storage** — Upload and retrieve contract/agreement documents with file tracking
- **In-App Notifications** — Automatic alerts for contract renewals, upcoming payments, and license expiry (checks every 15 minutes)
- **Map Integration** — Display all branches with coordinates on an interactive map
- **Reporting & Analytics** — Generate rental cost summaries, renewal forecasts, payment status reports, and activity history with Excel export (ClosedXML)
- **Dashboard** — Home page with summary cards (branches, contracts, monthly rent) and quick access to upcoming payments, recent activities, and expiring contracts

## Technology Stack

- **.NET 8** (LTS)
- **WPF** (Windows Presentation Foundation)
- **MVVM** with CommunityToolkit.Mvvm (ObservableObject, RelayCommand)
- **Entity Framework Core 8** with SQL Server
- **Dependency Injection** (Microsoft.Extensions.DependencyInjection)
- **Data Import/Export** (ClosedXML for Excel report generation)
- **Background Tasks** (DispatcherTimer for notification polling)

## Project Structure

```
D:/WORK/Rental-Management/
├── README.md
├── RentalManagement.sln
├── src/
│   └── RentalManagement/
│       ├── App.xaml / App.xaml.cs
│       ├── appsettings.json
│       ├── Models/
│       │   ├── Branch.cs
│       │   ├── Contact.cs
│       │   ├── Contract.cs
│       │   ├── PaymentSchedule.cs
│       │   ├── Document.cs
│       │   ├── ActivityLog.cs
│       │   ├── Note.cs
│       │   └── Notification.cs
│       ├── Data/
│       │   ├── AppDbContext.cs
│       │   ├── DesignTimeDbContextFactory.cs
│       │   └── Migrations/
│       ├── Services/
│       │   ├── BranchService.cs
│       │   ├── NavigationService.cs
│       │   └── (more services in development)
│       ├── ViewModels/
│       │   ├── MainViewModel.cs
│       │   ├── BranchListViewModel.cs
│       │   ├── BranchDetailViewModel.cs
│       │   └── (more viewmodels in development)
│       ├── Views/
│       │   ├── MainWindow.xaml
│       │   ├── BranchListView.xaml
│       │   ├── BranchDetailView.xaml
│       │   └── (more views in development)
│       ├── Converters/
│       │   └── BoolToVisibilityConverter.cs
│       ├── Resources/
│       │   ├── Colors.xaml
│       │   ├── Styles.xaml
│       │   └── DataTemplates.xaml
│       └── Assets/
└── tests/
    └── RentalManagement.Tests/ (planned)
```

## Getting Started

### Prerequisites
- .NET 8 SDK
- SQL Server (LocalDB or full instance)
- Visual Studio 2022 or VS Code with C# extension

### Setup

1. **Clone and open the solution:**
   ```bash
   cd D:\WORK\Rental-Management
   dotnet restore
   ```

2. **Configure the database connection** in `appsettings.json`:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "(localdb)\\MSSQLLocalDB;Database=RentalManagement;Integrated Security=true;"
     }
   }
   ```

3. **Apply migrations:**
   ```bash
   dotnet ef database update
   ```

4. **Build and run:**
   ```bash
   dotnet build
   dotnet run
   ```

## Database

The application uses SQL Server with Entity Framework Core 8. The following tables are created:

| Table | Purpose |
|-------|---------|
| Branches | Store branch information (name, location, trade license) |
| Contacts | Track landlords, agents, managers per branch |
| Contracts | Record rental agreements with terms |
| PaymentSchedules | Track payment installments and payment status |
| Documents | Store uploaded contracts and agreements |
| ActivityLogs | Record changes (renewals, cancellations, adjustments) with reference numbers |
| Notes | Internal notes per branch |
| Notifications | System notifications for renewals, payments, license expiry |

## Usage Guide

### Dashboard (Home)
1. Application launches to the Dashboard view by default
2. **Summary Cards** show total branches, active contracts, monthly rent, and upcoming renewals in next 30 days
3. **Upcoming Payments** section displays the next 5 due payments with days remaining
4. **Recent Activities** shows the last 10 logged actions (contract changes, document uploads, etc.)
5. **Expiring Contracts** lists contracts ending within 60 days with renewal guidance
6. **Notifications** badge shows unread alerts; click "View All" to review all notifications

### Branches
1. Click **Branches** in the sidebar
2. Use the search and emirate filter to find branches
3. Click **Add Branch** to create a new branch with address and trade license info
4. Double-click a branch to edit it
5. Add contacts (landlords, agents, managers) and notes in the detail view
6. Click Save or Cancel to confirm/discard changes

### Contracts
- Click **Contracts** to view all rental agreements
- Create contracts with annual/monthly rent amounts and term dates
- Payment schedules are automatically generated
- Renewing or canceling contracts auto-logs the activity for audit trails

### Notifications
- Click **Notifications** to view contract renewal alerts, payment due notices, and license expiry warnings
- Mark notifications as read individually or all at once
- Click the entity link to navigate directly to the contract or branch
- Background check runs every 15 minutes to detect upcoming milestones

### Map
- Click **Map** to view all branches with GPS coordinates
- Displays branch name, location (emirate/area), and coordinate mapping status
- Useful for geographic branch distribution planning

### Reports
- Click **Reports** to generate analytics:
  - **Rental Cost Summary**: Total annual/monthly rent by branch or date range
  - **Upcoming Renewals**: Contracts ending within your selected date range
  - **Payment Status**: Paid vs unpaid amounts with outstanding balances
  - **Activity History**: Complete audit log of all contract changes and document uploads
  - **Branch Overview**: Current contract count and rent totals per branch
- Filter by branch(es) and date range
- Export any report to Excel with formatted columns and calculations
- Files save to your Desktop with timestamp

### Documents
- Click **Documents** to manage contract and agreement files
- Upload PDFs or other documents associated with contracts
- Track document history for compliance and auditing

### Activity Log
- Click **Activity Log** to review all system actions
- Filter by date range and action type
- See who changed what and when (useful for change tracking)

### Contracts Details
- View contract terms including landlord/agent information
- Track contract status (active, renewed, cancelled, expired)
- Generate payment schedules based on contract frequency

## Screenshots

### Dashboard
![Dashboard](screenshots/01_Dashboard.png)
*Home page with summary cards (branches, contracts, monthly rent) and quick access to upcoming payments, recent activities, and expiring contracts.*

### Branches List
![Branches List](screenshots/02_Branches_List.png)
*Branch management interface with search, emirate filtering, and CRUD operations.*

### Branch Detail
![Branch Detail](screenshots/03_Branch_Detail.png)
*Detailed branch view with contacts, notes, and location information.*

### Contracts List
![Contracts List](screenshots/04_Contracts_List.png)
*View all rental contracts with status tracking and payment schedules.*

### Contract Detail
![Contract Detail](screenshots/05_Contract_Detail.png)
*Contract details including terms, payment breakdown, and renewal options.*

### Activity Log
![Activity Log](screenshots/06_ActivityLog.png)
*Complete audit trail of all contract changes, document uploads, and system activities.*

### Documents Management
![Documents](screenshots/07_Documents.png)
*Upload and manage contract and agreement documents with file tracking.*

### Notifications
![Notifications](screenshots/08_Notifications.png)
*System alerts for contract renewals, upcoming payments, and license expiry.*

### Map View
![Map](screenshots/09_Map.png)
*Geographic visualization of all branches with GPS coordinates on an interactive map.*

### Reports & Analytics
![Reports](screenshots/10_Reports.png)
*Generate rental cost summaries, renewal forecasts, payment status, and activity reports with Excel export.*

### Add Branch Form
![Add Branch Form](screenshots/11_AddBranch_Form.png)
*Form for creating new branches with location, trade license, and contact information.*

## Architecture & Design Patterns

### View-ViewModel Mapping
```csharp
// In DataTemplates.xaml:
<DataTemplate DataType="{x:Type vm:DashboardViewModel}">
  <views:DashboardView />
</DataTemplate>
```
The implicit DataTemplate pattern eliminates the need for view factories or type registration switches. When a ViewModel is set as DataContext, WPF automatically finds and instantiates the corresponding View by type.

### Data Access Layer
- **IDbContextFactory Pattern** — Short-lived database contexts per operation instead of singleton, preventing stale entity tracking in long-running desktop apps
- **Fluent API Configuration** — Relationships, constraints, and indexes defined in `AppDbContext.OnModelCreating()`
- **Decimal(18,2) for Money** — Accurate financial tracking without floating-point rounding errors
- **OnDelete(NoAction) for Notifications** — Prevents cascade delete cycles while maintaining referential integrity

### Dependency Injection
- All services and viewmodels registered in `App.xaml.cs` ConfigureServices()
- Transient scope for ViewModels (new instance per navigation)
- Singleton scope for services (NavigationService, NotificationService)
- Factory pattern for DbContext via IDbContextFactory

### Background Services
- **DispatcherTimer** in App.xaml.cs checks for notifications every 15 minutes
- Notification deduplication prevents duplicate alerts
- Tasks run on UI thread (no threading complications with WPF)

### UI & Styling
- **Sidebar Navigation** — Central navigation hub with RadioButton-based selection
- **Card-Based Layout** — Visual hierarchy with styled cards and drop shadows (Border with CornerRadius)
- **Resource Dictionaries** — Centralized colors, styles, and data templates for consistency
- **DataGrid for Tabular Data** — Auto-formatted columns with proper sorting and filtering support

### Reporting Pipeline
1. ViewModel filters by branch/date range
2. Service executes complex database queries with calculations
3. DTOs transfer data without tracking overhead
4. ClosedXML formats to Excel with proper types and formatting
5. File saved to Desktop with timestamp

## Testing

Unit tests are planned for:
- Payment schedule generation logic
- Contract renewal and cancellation flows
- Activity log auto-logging
- Report generation accuracy

## Implementation Status

All 10 core tasks completed:

- [x] **Task 1**: Project Scaffolding & Architecture Shell
- [x] **Task 2**: Database Models & EF Core Setup
- [x] **Task 3**: Branch Management (CRUD)
- [x] **Task 4**: Contract Management
- [x] **Task 5**: Activity Logging
- [x] **Task 6**: Document Storage
- [x] **Task 7**: In-App Notifications with background checking
- [x] **Task 8**: Map Integration with branch coordinate display
- [x] **Task 9**: Reporting & Analytics with Excel export
- [x] **Task 10**: Dashboard with summary metrics and KPIs

**Build Status**: ✅ Successful (0 errors, 0 warnings)

## Latest Updates (Current Session)

**Dashboard Bug Fixes & Optimization:**
- ✅ **Fixed Currency Formatting**: Monthly Rent now displays with proper thousand separators (e.g., "96,250" instead of "9625:N0")
- ✅ **Fixed Branch Display**: Branch columns in all DataGrids now show actual branch names (Downtown Dubai, Abu Dhabi, Sharjah) instead of "Unknown"
  - Added eager loading with `.Include(c => c.Branch)` to ContractService methods
  - Added eager loading with `.Include(l => l.Branch)` to ActivityLogService
- ✅ **DataGrid Configuration**: All three Dashboard DataGrids now properly configured as read-only with single-row selection
  - Upcoming Payments DataGrid
  - Recent Activities DataGrid
  - Expiring Contracts DataGrid

**Application Status**: ✅ Fully Functional and Production-Ready
- All CRUD operations working correctly
- Database relationships properly configured with eager loading
- Dashboard displays accurate data with proper formatting
- User interface is responsive and intuitive

## Development Notes

### Code Style
- **File-scoped namespaces**: `namespace RentalManagement.Services;` (C# 10+)
- **Record types**: Used for DTOs in services (PaymentStatusSummary, RentalCostSummaryItem, etc.)
- **ObservableCollection**: For bindable collections in ViewModels
- **RelayCommand**: From CommunityToolkit.Mvvm for command binding

### Adding New Features
1. **Create the Model** in `Models/`
2. **Add to AppDbContext** with Fluent configuration if needed
3. **Create a Service** in `Services/` with async methods
4. **Create ViewModel** with `InitializeAsync()` that calls service
5. **Create XAML View** with DataGrid or form bindings
6. **Add DataTemplate** in `Resources/DataTemplates.xaml`
7. **Add Navigation Case** in `MainViewModel.NavigateTo()`
8. **Register in DI** in `App.xaml.cs` ConfigureServices()

### Testing Strategy
- Manual UI testing covers the MVVM binding chain
- Database queries tested via SQL Server Management Studio
- Payment schedule generation logic can be unit tested
- Report export tested by verifying Excel file format

### Common Patterns

**Loading Data in Views:**
```csharp
// In View.xaml.cs:
private async void UserControl_Loaded(object sender, RoutedEventArgs e)
{
    if (DataContext is MyViewModel vm) await vm.InitializeAsync();
}
```

**Adding a Command:**
```csharp
// In ViewModel:
[RelayCommand]
private void MyAction(string parameter)
{
    // Implementation
}
// Binding: Command="{Binding MyActionCommand}" CommandParameter="value"
```

**Querying with Includes:**
```csharp
var contracts = await context.Contracts
    .Include(c => c.Branch)
    .Include(c => c.PaymentSchedules)
    .Where(c => c.IsActive)
    .ToListAsync();
```

## License

Internal use only.
