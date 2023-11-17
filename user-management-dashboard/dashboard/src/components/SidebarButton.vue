<template>
  <button class="sidebar-button" type="button">
    <slot></slot>
  </button>
</template>

<style scoped>
.sidebar-button {
  margin-bottom: 10px;
  padding: 10px 15px;
  background-color: #1a936f; /* Green button */
  border: 1px solid #1a936f;
  cursor: pointer;
  text-align: center;
  width: 100%;
  text-decoration:none;
  color: hsl(0, 10%, 14%); /* White text */
  font-weight: bold;
}

.sidebar-button:hover {
  background-color: #1a936f; /* Light green on hover */
}
</style>
