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
      </div>
    </section>

    <section class="role-specific-data">
      <h3>{{ userRoleSpecificData.title }}</h3>
      <ul>
        <li v-for="item in userRoleSpecificData.data" :key="item.id">
          <span>{{ item.details }}</span>
        </li>
      </ul>
    </section>

    <section class="recent-bugs">
      <h3>Recent Bugs</h3>
      <ul>
        <li v-for="bug in recentBugs" :key="bug.id">
          <span>{{ bug.details }}</span>
        </li>
      </ul>
    </section>

    <section class="assigned-bugs" v-if="assignedBugs.length > 0">
      <h3>Assigned Bugs</h3>
      <ul>
        <li v-for="bug in assignedBugs" :key="bug.id">
          <span>{{ bug.details }}</span>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userType: 'Technician', // Example: Set this based on your authentication logic
      stats: {
        totalBugs: 0,
        openBugs: 0,
        closedBugs: 0
      },
      recentBugs: [],
      pendingAssignments: [],
      assignedBugs: []
    }
  },
  computed: {
    userRoleSpecificData() {
      let result = {}
      if (this.userType === 'Employee') {
        result = {
          title: 'Your Submitted Bugs',
          data: this.recentBugs
        }
      } else if (this.userType === 'Administrator') {
        result = {
          title: 'Pending Bug Assignments',
          data: this.pendingAssignments
        }
      } else if (this.userType === 'Technician') {
        result = {
          title: 'Your Assigned Bugs',
          data: this.assignedBugs
        }
      } else {
        result = {
          title: '',
          data: []
        }
      }
      console.log('Computed userRoleSpecificData:', result) // Log computed property output
      return result
    }
  },
  mounted() {
    console.log('User type:', this.userType) // Log userType
    this.fetchStats()
    this.fetchRecentBugs()
    if (this.userType === 'Administrator' || this.userType === 'Technician') {
      this.fetchPendingAssignments()
    }
    if (this.userType === 'Technician') {
      this.fetchAssignedBugs()
    }
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
    async fetchPendingAssignments() {
      try {
        const response = await axios.get('/api/assignments/pending')
        this.pendingAssignments = response.data
        console.log('Pending Assignments:', this.pendingAssignments) // Log fetched pending assignments
      } catch (error) {
        console.error('Failed to fetch pending assignments:', error)
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
}

.dashboard-view .stat {
  background-color: #f1f1f1;
  padding: 10px;
  border-radius: 5px;
  text-align: center;
  flex: 1;
}

.dashboard-view .stat p {
  margin: 0;
  font-size: 18px;
  color: #555;
}

.dashboard-view .role-specific-data,
.dashboard-view .recent-bugs,
.dashboard-view .assigned-bugs {
  margin-bottom: 30px;
  padding: 20px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.dashboard-view .role-specific-data ul,
.dashboard-view .recent-bugs ul,
.dashboard-view .assigned-bugs ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.dashboard-view .role-specific-data h3,
.dashboard-view .recent-bugs h3,
.dashboard-view .assigned-bugs h3 {
  font-size: 22px;
  color: #555;
  margin-bottom: 10px;
}

.dashboard-view .role-specific-data ul li,
.dashboard-view .recent-bugs ul li,
.dashboard-view .assigned-bugs ul li {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.dashboard-view .role-specific-data ul li:last-child,
.dashboard-view .recent-bugs ul li:last-child,
.dashboard-view .assigned-bugs ul li:last-child {
  border-bottom: none;
}

.dashboard-view .role-specific-data ul li,
.dashboard-view .recent-bugs ul li,
.dashboard-view .assigned-bugs ul li {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.dashboard-view .role-specific-data ul li span,
.dashboard-view .recent-bugs ul li span,
.dashboard-view .assigned-bugs ul li span {
  flex: 1;
  text-align: left;
}

.dashboard-view .role-specific-data ul li span:last-child,
.dashboard-view .recent-bugs ul li span:last-child,
.dashboard-view .assigned-bugs ul li span:last-child {
  text-align: right;
}

.dashboard-view .role-specific-data ul li button,
.dashboard-view .recent-bugs ul li button,
.dashboard-view .assigned-bugs ul li button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.dashboard-view .role-specific-data ul li button:hover,
.dashboard-view .recent-bugs ul li button:hover,
.dashboard-view .assigned-bugs ul li button:hover {
  background-color: #0056b3;
}
</style>
