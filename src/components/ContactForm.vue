<template>
    <div class="contact-container">
      <form @submit.prevent="sendEmail">
        <label for="name">Name</label>
        <input type="text" id="name" v-model="name">
        <div class="error" v-if="errors.name">{{ errors.name }}</div>
        <div class="input_separator"></div>
        <label for="email">Email</label>
        <input type="email" id="email" v-model="email">
        <div class="error" v-if="errors.email">{{ errors.email }}</div>
        <div class="input_separator"></div>
        <label for="message">Message</label>
        <textarea id="message" v-model="message"></textarea>
        <div class="error" v-if="errors.message">{{ errors.message }}</div>
        <div class="input_separator"></div> 
        <button type="submit">Send</button>
      </form>
  
      <div v-if="successMessage">
        {{ successMessage }} <span style="color:green">✔</span>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        message: '',
        errors: {},
        successMessage: ''
      };
    },
    methods: {
      sendEmail() {
        this.errors = {};
  
        if (this.name.length < 2) {
          this.errors.name = "Is that really your name?";
        }
        if (!this.email.includes('@') || this.email.endsWith('@mailinator.com')) {
          this.errors.email = "Invalid email or email from blocked domain.";
        }
        if (!this.message) {
          this.errors.message = "Message cannot be empty.";
        }
  
        if (Object.keys(this.errors).length === 0) {
          // Mock sending email
          this.successMessage = "Your message has been sent!";
          this.name = '';
          this.email = '';
          this.message = '';
        }
      }
    }
  };
  </script>
  
  <style scoped>
.contact-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

input[type="text"], input[type="email"], textarea {
  display: block;
  width: 400px;
  border: none;
  border-bottom: 1px solid #333;
  padding: 0.5rem;
}

.input_separator {
    height: 2.5rem;
}

button {
  display: block;
  margin: 0 auto;
  background-color: #004d00;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s;

  &:hover {
    background-color: #003300;
  }
}

.error {
  color: red;
  font-size: 12px;
  margin-bottom: 1rem;
}
</style>
