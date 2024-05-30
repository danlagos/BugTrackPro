# Component: DashboardView

**Description**: Central hub for all users, showing relevant information based on user role.

## Data properties

- `userType`: String indicating the type of logged-in user (Employee, Administrator, Technician)
- `stats`: Object to store high-level statistics (e.g., total bugs, open bugs, closed bugs)
  - `totalBugs: 0`
  - `openBugs: 0`
  - `closedBugs: 0`
- `recentBugs`: Array to store the most recent bug reports
- `pendingAssignments`: Array to store pending bug assignments for administrators and technicians

## Lifecycle hook: onMounted

**Description**: Fetch initial data based on user role when the component is mounted.

```pseudo
onMounted():
  fetchStats()
  fetchRecentBugs()
  if userType == "Administrator" or userType == "Technician":
    fetchPendingAssignments()
```

## Methods

fetchStats():
GET /api/stats
Success:
stats = response.data
Error:
handle error

fetchRecentBugs():
GET /api/bugs/recent
Success:
recentBugs = response.data
Error:
handle error

fetchPendingAssignments():
GET /api/assignments/pending
Success:
pendingAssignments = response.data
Error:
handle error

## Computed properties

userRoleSpecificData:
if userType == "Employee":
return {
title: "Your Submitted Bugs",
data: recentBugs
}
else if userType == "Administrator":
return {
title: "Pending Bug Assignments",
data: pendingAssignments
}
else if userType == "Technician":
return {
title: "Your Assigned Bugs",
data: pendingAssignments
}

### Key Points

- **Data Properties**: Stores user type, high-level statistics, recent bugs, and pending assignments.
- **Lifecycle Hook (onMounted)**: Fetches initial data based on user role when the component is mounted.
- **Methods**:
  - `fetchStats()`: Fetches high-level statistics for the dashboard.
  - `fetchRecentBugs()`: Fetches the most recent bug reports.
  - `fetchPendingAssignments()`: Fetches pending bug assignments for administrators and technicians.
- **Computed Properties**:
  - `userRoleSpecificData`: Provides data specific to the user role, such as recent bugs for employees, pending assignments for administrators, and assigned bugs for technicians.
- **Template Structure**:
  - Displays high-level statistics.
  - Shows user role-specific data.
  - Lists recent bugs for all users.

By following this pseudocode, the `DashboardView` component can provide a comprehensive overview of the application's status tailored to the different user roles.
