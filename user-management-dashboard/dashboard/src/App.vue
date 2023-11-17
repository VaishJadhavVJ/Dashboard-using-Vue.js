<template>
   <div id="app" class="flex h-screen">
    <!-- Sidebar -->
    <nav class="sidebar w-1/4 bg-green-600 py-4">
      <div class="sidebar-header text-white text-xl font-bold text-center mb-4">
        Welcome to Dasboard!!
      </div>

      <!-- Sidebar buttons -->
      <SidebarButton @click="scrollToSection('account-creation')">Create Account</SidebarButton>
      <SidebarButton @click="scrollToSection('user-details')">User Details</SidebarButton>
    </nav>

    <!-- Main Content -->
    <div class="main-content flex-1 overflow-x-hidden overflow-y-auto p-8 bg-gradient-to-r from-teal-100 to-gray-100">
      <!-- Account Creation Tab -->
      <div id="account-creation" class="tab mb-8">
        <AccountCreationTab :users="users" @create-account="createAccount" />
      </div>

      <!-- User Details Tab -->
      <div id="user-details" class="tab">
        <UserDetailsTab :users="users" @open-popup="openPopup" @close-popup="closePopup" @generate-report="generateReport" />
      </div>
    </div>
  </div>
</template>

<!-- Rest of the script and styles remain the same -->


<script>
import UserDetailsTab from '@/components/UserDetailsTab.vue';
import AccountCreationTab from '@/components/AccountCreationTab.vue';
import SidebarButton from '@/components/SidebarButton.vue'; 

export default {
  components: {
    UserDetailsTab,
    AccountCreationTab,
    SidebarButton,
  },
  data() {
    return {
      users: [],
      selectedUser: null,
    };
  },
  mounted() {
    this.fetchUserData();
  },
  methods: {
    scrollToSection(sectionId) {
      document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
    },
    openPopup(user) {
      this.selectedUser = user;
    },
    closePopup() {
      this.selectedUser = null;
    },
    generateReport(user) {
      console.log('generateReport method called with user:', user);
      this.selectedUser = user;
      // Add logic to open the popup
    },
    createAccount(newUser) {
      this.users.push(newUser);
    },
    async fetchUserData() {
      // Dummy data for testing
      this.users = [
        { id: 1, username: 'user1', email: 'user1@example.com', phone: '123-456-7890', creationDate: '2023-01-01' },
      ];
    },
  },
};
</script>

<style>
/* Updated styling for sidebar */

/* Add your component-specific styles here */

.container {
  background-image: url('assets/notebook.jpg'); /* Replace with your own image */
  background-size: cover;
}

/* For UserDetailsPopup.vue */
.user-detail-container {
  position: relative;
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  animation: fade-in 0.5s ease-in-out;
}

@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #fff; /* Dark green background */
  color: #020000; /* White text */
}
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 25%; /* Set width to 25% */
  background-color: #1a936f;
  color: #f3e9d2;
  padding: 20px;
}

.sidebar-header {
  font-size: 24px;
  text-align: center;
  color: #020000;
  text-shadow: #cdf4d6;
}

.sidebar-button {
  margin-bottom: 10px;
  padding: 10px 15px;
  background-color: #f3e9d2;
  border: 1px solid #f3e9d2;
  cursor: pointer;
  text-align: left;
  width: 100%;
  text-decoration: none;
  color: #cdf4d6;
  font-weight: bold;
}

.sidebar-button:hover {
  background-color: #f3e9d2;
}

/* Updated styling for main content area */
.main-content {
  padding: 40px;
  margin-left: 25%; /* Adjust margin to match the sidebar width */
  width: 75%; 
  display: flex;
  flex-direction: column;
}

/* Updated styling for individual tabs */
.tab {
  padding: 20px;
  border: 1px solid #000000;
  margin-bottom: 20px;
}
</style>

