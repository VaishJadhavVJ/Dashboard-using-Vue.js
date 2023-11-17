<template>
  <div>
    <h1 class="text-3xl font-bold mb-8 text-center text-indigo-700"><strong>Create Your Account</strong></h1>

    <form @submit.prevent="submitForm" class="max-w-md mx-auto p-8 bg-white rounded-lg shadow-md">
      <div class="mb-6">
        <label for="username" class="block text-gray-700 text-sm font-semibold mb-2">Username:</label>
        <input
          type="text"
          id="username"
          v-model="username"
          class="w-full py-2 px-4 border-b-2 border-indigo-500 focus:outline-none focus:border-indigo-700"
          required
        />
      </div>

      <div class="mb-6">
        <label for="email" class="block text-gray-700 text-sm font-semibold mb-2">Email:</label>
        <input
          type="email"
          id="email"
          v-model="email"
          class="w-full py-2 px-4 border-b-2 border-indigo-500 focus:outline-none focus:border-indigo-700"
          required
        />
      </div>

      <div class="mb-6">
        <label for="phone" class="block text-gray-700 text-sm font-semibold mb-2">Phone Number:</label>
        <input
          type="tel"
          id="phone"
          v-model="phone"
          class="w-full py-2 px-4 border-b-2 border-indigo-500 focus:outline-none focus:border-indigo-700"
          required
        />
      </div>

      <div class="mb-6">
        <label for="password" class="block text-gray-700 text-sm font-semibold mb-2">Password:</label>
        <input
          type="password"
          id="password"
          v-model="password"
          @input="checkPasswordStrength"
          class="w-full py-2 px-4 border-b-2 border-indigo-500 focus:outline-none focus:border-indigo-700"
          required
        />
        <span v-if="password" :class="passwordStrengthClass" class="text-sm mt-2">{{ passwordStrength }}</span>
      </div>

      <div class="mb-6">
        <label for="repeatPassword" class="block text-gray-700 text-sm font-semibold mb-2">Repeat Password:</label>
        <input
          type="password"
          id="repeatPassword"
          v-model="repeatPassword"
          class="w-full py-2 px-4 border-b-2 border-indigo-500 focus:outline-none focus:border-indigo-700"
          required
        />
      </div>

      <button
        type="submit"
        :disabled="!isPasswordValid"
        class="w-full bg-indigo-500 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded focus:outline-none"
      >
        Create Account
      </button>

      <div v-if="accountCreated" class="mt-4 text-center">
        <p class="text-green-500">Account successfully created!</p>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    users: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      username: '',
      email: '',
      phone: '',
      password: '',
      repeatPassword: '',
      isPasswordValid: false,
      passwordStrength: '',
      accountCreated: false,
    };
  },
  methods: {
    submitForm() {
      // Check if passwords match and email is valid before creating the account
      if (this.password === this.repeatPassword && this.isValidEmail(this.email)) {
        const newUser = {
          id: this.users.length + 1,
          username: this.username,
          email: this.email,
          phone: this.phone,
          creationDate: new Date().toLocaleDateString(),
        };

        // Emit an event to create the account in the parent component
        this.$emit('create-account', newUser);

        // Reset form fields and flags
        this.username = '';
        this.email = '';
        this.phone = '';
        this.password = '';
        this.repeatPassword = '';
        this.isPasswordValid = false;
        this.passwordStrength = '';
        this.accountCreated = true;

        // Close the success message after a delay
        setTimeout(() => {
          this.accountCreated = false;
        }, 3000);
      } else if (!this.isValidEmail(this.email)) {
        alert('Invalid email address. Please enter a valid email address.');
      } else {
        alert('Passwords do not match. Please enter matching passwords.');
      }
    },
    checkPasswordStrength() {
      const passwordLength = this.password.length;

      if (passwordLength < 6) {
        this.passwordStrength = 'Weak';
        this.isPasswordValid = false;
      } else if (passwordLength < 10) {
        this.passwordStrength = 'Moderate';
        this.isPasswordValid = true;
      } else {
        this.passwordStrength = 'Strong';
        this.isPasswordValid = true;
      }
    },
    isValidEmail(email) {
      const regex = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;
      return regex.test(email);
    },
  },
  computed: {
    passwordStrengthClass() {
      return {
        'text-red-500': this.passwordStrength === 'Weak',
        'text-orange-500': this.passwordStrength === 'Moderate',
        'text-green-500': this.passwordStrength === 'Strong',
      };
    },
  },
};
</script>

<style>

.container {
  background-color: rgb(26, 133, 37); /* White background */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  overflow: hidden;
}

.text-center {
  text-align: center;
  font-size: 24px;
  color: #114b5f; /* Primary color */
}

.mb-2 {
  margin-bottom: 0.5rem;
  text-align: center;
}

.mb-4 {
  margin-bottom: 1.5rem;
}

.mb-6 {
  margin-bottom: 2.0rem;
}

.mt-2 {
  margin-top: 0.5rem;
}

.mt-4 {
  margin-top: 1rem;
}

.w-full {
  width: 100%;
}

.py-2 {
  padding-top: 0.5rem;
  padding-bottom: 1rem;
}

.px-4 {
  padding-left: 2rem;
  padding-right: 1rem;
}

.border-b-2 {
  border-bottom-width: 3px;
}

.focus\:outline-none:focus {
  outline: none;
}

.focus\:border-indigo-700:focus {
  border-color: #4a5568; /* Primary color shade */
}

.bg-white {
  background-color: #fff;
}

.rounded-lg {
  border-radius: 0.5rem;
}

.shadow-md {
  box-shadow: 0 4px 6px -1px rgba(255, 254, 254, 0.1), 0 2px 4px -1px rgba(253, 253, 253, 0.06);
}

.text-indigo-700 {
  color: #4a6853; /* Primary color shade */
}

.border-indigo-500 {
  border-color: rgb(45, 72, 58); /* Primary color */
}

.border-indigo-500:hover {
  border-color: #4a5568; /* Primary color shade */
}

.bg-indigo-500 {
  background-color: #005108; /* Primary color */
}

.bg-indigo-500:hover {
  background-color: rgb(8, 123, 54); /* Primary color tint */
}

.text-white {
  color: #0a0000;
}

.hover\:bg-indigo-700:hover {
  background-color: rgb(26, 133, 37); /* Primary color shade with darker tone */
}

.hover\:text-white:hover {
  color: #280303; /* Primary color shade with darker tone */
}

.text-red-500 {
  color: red;
}

.text-orange-500 {
  color: orange;
}

.text-green-500 {
  color: green;
}


</style>