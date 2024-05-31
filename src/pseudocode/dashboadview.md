# Pseudocode for DashboardView Component

## Template Structure

**Description**: Provides an overview of the application's status, including summaries of bug reports and assignments.

- Create a `div` element with a class of `dashboard-view`.
  - Inside the `div`, create a `section` element with a class of `stats`.
    - Inside the `section`, create an `h2` element with the text "Dashboard".
    - Inside the `section`, create a `div` element with a class of `stats-block`.
      - Inside the `div`, create multiple `div` elements with a class of `stat` for each statistic:
        - Each `stat` contains:
          - A `p` element with the text "Total Bugs" and another `p` element displaying `stats.totalBugs`.
          - A `p` element with the text "Open Bugs" and another `p` element displaying `stats.openBugs`.
          - A `p` element with the text "Closed Bugs" and another `p` element displaying `stats.closedBugs`.
          - A `p` element with the text "Recent Bugs" and another `p` element displaying the length of `recentBugs`.
          - A `p` element with the text "Assigned Bugs" and another `p` element displaying the length of `assignedBugs`.

## Script Section

**Description**: Defines data properties, lifecycle hooks, and methods for fetching data from the API.

### Data Properties

- `stats`: An object to store statistics about bugs.
  - `totalBugs`: Number of total bugs.
  - `openBugs`: Number of open bugs.
  - `closedBugs`: Number of closed bugs.
- `recentBugs`: An array to store recent bug reports.
- `assignedBugs`: An array to store assigned bugs.

### Lifecycle Hooks

- `mounted`: A lifecycle hook that calls methods to fetch data when the component is mounted.
  - Calls `fetchStats()`
  - Calls `fetchRecentBugs()`
  - Calls `fetchAssignedBugs()`

### Methods

- `fetchStats`: Fetches statistics about bugs from the API.
  - Makes a GET request to the `/api/stats` endpoint.
  - On success, updates the `stats` data property with the response data.
  - Logs the fetched stats.
  - On error, logs an error message.
- `fetchRecentBugs`: Fetches recent bug reports from the API.
  - Makes a GET request to the `/api/bugs/recent` endpoint.
  - On success, updates the `recentBugs` data property with the response data.
  - Logs the fetched recent bugs.
  - On error, logs an error message.
- `fetchAssignedBugs`: Fetches assigned bugs from the API.
  - Makes a GET request to the `/api/bugs/assigned` endpoint.
  - On success, updates the `assignedBugs` data property with the response data.
  - Logs the fetched assigned bugs.
  - On error, logs an error message.

## Style Section

**Description**: Defines styles for the dashboard view, including layout and appearance of statistics.

- Apply styles scoped to the `dashboard-view` component:
  - `.dashboard-view` class:
    - Sets font-family to Arial, sans-serif.
    - Adds padding of 20px.
    - Sets background-color to #f9f9f9.
  - `h2` element inside `.dashboard-view`:
    - Sets color to #333.
    - Adds margin-bottom of 20px.
    - Centers the text.
  - `.stats` class inside `.dashboard-view`:
    - Adds margin-bottom of 30px.
    - Adds padding of 20px.
    - Sets background-color to #fff.
    - Adds border of 1px solid #ddd.
    - Sets border-radius to 8px.
    - Adds box-shadow of 0 2px 4px rgba(0, 0, 0, 0.1).
  - `.stats-block` class inside `.dashboard-view`:
    - Uses flexbox to center the content.
    - Adds gap of 20px.
    - Allows wrapping of items.
  - `.stat` class inside `.stats-block`:
    - Sets background-color to #f1f1f1.
    - Adds padding of 10px.
    - Sets border-radius to 5px.
    - Centers the text.
    - Sets flex property to 1 1 150px (adjust width as needed).
  - `p` elements inside `.stat`:
    - Removes margin.
    - Sets font-size to 18px.
    - Sets color to #555.
