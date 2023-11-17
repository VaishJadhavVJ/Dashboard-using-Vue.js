<template>
    <div class="bg-gray-100 p-4">
      <h2 class="text-2xl font-bold mb-4">User Information</h2>
  
      <!-- Table structure for user information -->
      <div class="overflow-x-auto">
        <table class="min-w-full bg-white border border-gray-300">
          <thead>
            <tr class="bg-gray-200">
              <th class="py-3 px-4 border-b">Username</th>
              <th class="py-3 px-4 border-b">Email</th>
              <th class="py-3 px-4 border-b">Phone</th>
              <th class="py-3 px-4 border-b">ID</th>
              <th class="py-3 px-4 border-b">Creation Date</th>
            </tr>
          </thead>
          <tbody>
            <!-- Loop through user data and display rows -->
            <tr v-for="user in users" :key="user.id" @click="openDetailsPopup(user)" class="cursor-pointer hover:bg-gray-100 transition">
              <td class="py-2 px-4 border-b">{{ user.username }}</td>
              <td class="py-2 px-4 border-b">{{ user.email }}</td>
              <td class="py-2 px-4 border-b">{{ user.phone }}</td>
              <td class="py-2 px-4 border-b">{{ user.id }}</td>
              <td class="py-2 px-4 border-b">{{ user.creationDate }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      // Define the users prop to pass user data to this component
      users: {
        type: Array,
        required: true,
      },
    },
    methods: {
      openDetailsPopup(user) {
        // Emit an event to open the UserDetailsPopup with the selected user
        this.$emit('open-popup', user);
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add your component-specific styles here */
  .action-button:hover {
    background-color: #4a9a4d; /* Change hover color for better visibility */
  }
  </style>
  