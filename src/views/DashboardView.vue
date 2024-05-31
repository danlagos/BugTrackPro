<template>
  <div class="dashboard-view">
    <section class="stats">
      <h2>Dashboard</h2>
      <div class="stats-block">
        <div class="stat">
          <p>Total Bugs</p>
          <p>{{ stats.totalBugs }}</p>
        </div>
        <div class="stat">
          <p>Open Bugs</p>
          <p>{{ stats.openBugs }}</p>
        </div>
        <div class="stat">
          <p>Closed Bugs</p>
          <p>{{ stats.closedBugs }}</p>
        </div>
        <div class="stat">
          <p>Recent Bugs</p>
          <p>{{ recentBugs.length }}</p>
        </div>
        <div class="stat">
          <p>Assigned Bugs</p>
          <p>{{ assignedBugs.length }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      stats: {
        totalBugs: 0,
        openBugs: 0,
        closedBugs: 0
      },
      recentBugs: [],
      assignedBugs: []
    }
  },
  mounted() {
    this.fetchStats()
    this.fetchRecentBugs()
    this.fetchAssignedBugs()
  },
  methods: {
    async fetchStats() {
      try {
        const response = await axios.get('/api/stats')
        this.stats = response.data
        console.log('Stats:', this.stats) // Log fetched stats
      } catch (error) {
        console.error('Failed to fetch stats:', error)
      }
    },
    async fetchRecentBugs() {
      try {
        const response = await axios.get('/api/bugs/recent')
        this.recentBugs = response.data
        console.log('Recent Bugs:', this.recentBugs) // Log fetched recent bugs
      } catch (error) {
        console.error('Failed to fetch recent bugs:', error)
      }
    },
    async fetchAssignedBugs() {
      try {
        const response = await axios.get('/api/bugs/assigned')
        this.assignedBugs = response.data
        console.log('Assigned Bugs:', this.assignedBugs) // Log fetched assigned bugs
      } catch (error) {
        console.error('Failed to fetch assigned bugs:', error)
      }
    }
  }
}
</script>

<style scoped>
/* DashboardView Styles */
.dashboard-view {
  font-family: Arial, sans-serif;
  padding: 20px;
  background-color: #f9f9f9;
}

.dashboard-view h2 {
  color: #333;
  margin-bottom: 20px;
  text-align: center;
}

.dashboard-view .stats {
  margin-bottom: 30px;
  padding: 20px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.dashboard-view .stats-block {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.dashboard-view .stat {
  background-color: #f1f1f1;
  padding: 10px;
  border-radius: 5px;
  text-align: center;
  flex: 1 1 150px; /* Adjust width as needed */
}

.dashboard-view .stat p {
  margin: 0;
  font-size: 18px;
  color: #555;
}
</style>
