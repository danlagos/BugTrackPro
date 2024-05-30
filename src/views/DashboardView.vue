<template>
  <div class="dashboard-view">
    <section class="stats">
      <h2>Dashboard</h2>
      <p>Total Bugs: {{ stats.totalBugs }}</p>
      <p>Open Bugs: {{ stats.openBugs }}</p>
      <p>Closed Bugs: {{ stats.closedBugs }}</p>
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
      userType: '',
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
      if (this.userType === 'Employee') {
        return {
          title: 'Your Submitted Bugs',
          data: this.recentBugs
        }
      } else if (this.userType === 'Administrator') {
        return {
          title: 'Pending Bug Assignments',
          data: this.pendingAssignments
        }
      } else if (this.userType === 'Technician') {
        return {
          title: 'Your Assigned Bugs',
          data: this.assignedBugs
        }
      } else {
        return {
          title: '',
          data: []
        }
      }
    }
  },
  mounted() {
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
    fetchStats() {
      // Implement the API call to fetch stats
    },
    fetchRecentBugs() {
      // Implement the API call to fetch recent bugs
    },
    fetchPendingAssignments() {
      // Implement the API call to fetch pending assignments
    },
    fetchAssignedBugs() {
      // Implement the API call to fetch assigned bugs
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
}

.dashboard-view .stats,
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

.dashboard-view .stats p,
.dashboard-view .role-specific-data ul,
.dashboard-view .recent-bugs ul,
.dashboard-view .assigned-bugs ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.dashboard-view .stats p {
  font-size: 18px;
  color: #555;
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
