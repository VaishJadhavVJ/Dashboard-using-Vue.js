<template>
  <div class="user-detail-container" transition="fade-in-right" duration="300">
    <h2 class="text-xl font-bold text-gray-700 mb-4">User Details</h2>

    <table>
      <thead>
        <tr>
          <th class="text-gray-600 font-semibold">Field</th>
          <th class="text-gray-600 font-semibold">Value</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Username:</td>
          <td>{{ selectedUser.username }}</td>
        </tr>
        <tr>
          <td>Email:</td>
          <td>{{ selectedUser.email }}</td>
        </tr>
        <tr>
          <td>Phone:</td>
          <td>{{ selectedUser.phone }}</td>
        </tr>
        <tr>
          <td>ID:</td>
          <td>{{ selectedUser.id }}</td>
        </tr>
        <tr>
          <td>Creation Date:</td>
          <td>{{ selectedUser.creationDate }}</td>
        </tr>
      </tbody>
    </table>

    <div class="flex justify-between mt-4">
      <button @click="closePopup" class="btn-secondary">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectedUser: {
      type: Object,
      required: true,
    },
  },
  methods: {
    closePopup() {
      this.$emit('close-popup'); // Emit the same event that triggers the popup opening
    },
  },
};
</script>

<style scoped>
.user-detail-container {
  position: relative;
  background-color:#b2b6b2 ;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(250, 247, 247, 0.06);
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

.user-detail-container table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 5px;
  border: 1px solid #160202;
}

.btn-secondary {
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  font-weight: bold;
  background-color: #e7e7e7;
  color: #878787;
}
</style>
