<template>
  <div class="user-details-tab">
    <h1><strong>User Details</strong></h1>

    <div class="user-table">
      <table class="min-w-full">
        <thead>
          <tr>
            <th>Username</th>
            <th>Email</th>
            <th>Phone</th>
            <th>ID</th>
            <th>Creation Date</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id" @click="openDetailsPopup(user)">
            <td>{{ user.username }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.phone }}</td>
            <td>{{ user.id }}</td>
            <td>{{ user.creationDate }}</td>
            <td>
              <button class="btn btn-sm btn-primary" @click="openDetailsPopup(user)">
                View Details
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <user-details-popup v-if="selectedUser" :selected-user="selectedUser" @update-user="updateUser" @close-popup="closePopup" @generate-report="generateReport" />
  </div>
</template>

<script>
import UserDetailsPopup from '@/components/UserDetailsPopup.vue';

export default {
  components: {
    UserDetailsPopup,
  },
  props: {
    users: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      selectedUser: null,
    };
  },
  methods: {
    openDetailsPopup(user) {
      this.selectedUser = user;
    },
    closePopup() {
      this.selectedUser = null;
    },
    updateUser(user) {
      // Update the user data here
      console.log('User updated:', user);
    },
    generateReport(user) {
      console.log('Generating report for user:', user);
    },
    scrollToSection(sectionId) {
      document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
    },
  },
};
</script>

<style scoped>
.container {
  background-color: #fff; /* White background */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  overflow: hidden;
  align-items: center;
}
.user-details-tab h1 {
  text-align: center;
  font-size: 24px;
  color: #114b5f;
}

.user-table {
  padding: 20px;
  border: 1px solid #080101;
  border-collapse: collapse;
  background-color: #f0f0f0;
  text-align: center;
  align-items: center;
}
.user-table th,
.user-table td {
  padding: 10px;
  border: 1px solid #140202;
  text-align: center;
  background-color: #ffffff;
  align-items: center;
}
.btn-primary{
  background-color: aquamarine;
}
</style>
