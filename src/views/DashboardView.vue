<template>
    <div class="dashboard">
      <h1>Dashboard</h1>
      <div class="summary">
        <div class="summary-item">
          <h2>Total Bugs</h2>
          <p>123</p>
        </div>
        <div class="summary-item">
          <h2>Assigned Bugs</h2>
          <p>45</p>
        </div>
        <div class="summary-item">
          <h2>Open Bugs</h2>
          <p>67</p>
        </div>
        <div class="summary-item">
          <h2>Closed Bugs</h2>
          <p>56</p>
        </div>
      </div>
      <div class="recent-activity">
        <h2>Recent Activity</h2>
        <ul>
          <li>Bug #1234: Fixed by Technician A</li>
          <li>Bug #1235: Assigned to Technician B</li>
          <li>Bug #1236: Submitted by Employee C</li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'DashboardView'
  };
  </script>
  
  <style scoped>
  .dashboard {
    max-width: 800px;
    margin: 0 auto;
    padding: 2em;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  
  h1 {
    text-align: center;
    margin-bottom: 1em;
  }
  
  .summary {
    display: flex;
    justify-content: space-around;
    margin-bottom: 2em;
  }
  
  .summary-item {
    background-color: #fff;
    padding: 1em;
    border: 1px solid #ddd;
    border-radius: 8px;
    text-align: center;
    width: 150px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  }
  
  .summary-item h2 {
    margin-bottom: 0.5em;
    font-size: 1.2em;
  }
  
  .summary-item p {
    font-size: 1.5em;
    font-weight: bold;
    color: #007BFF;
  }
  
  .recent-activity {
    background-color: #fff;
    padding: 1em;
    border: 1px solid #ddd;
    border-radius: 8px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  }
  
  .recent-activity h2 {
    margin-bottom: 0.5em;
  }
  
  .recent-activity ul {
    list-style-type: none;
    padding: 0;
  }
  
  .recent-activity li {
    padding: 0.5em 0;
    border-bottom: 1px solid #ddd;
  }
  
  .recent-activity li:last-child {
    border-bottom: none;
  }
  </style>
  