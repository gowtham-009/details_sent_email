<template>
    <form @submit.prevent="sendEmail" class="w-100 h-screen pa-2 d-flex justify-center align-center flex-column">
      <div class="d-flex flex-column pa-1">
        <label for="name">Name</label>
        <input class="pa-2 rounded-sm " placeholder="Enter your name" style="border: 1px solid grey;" v-model="formData.name" type="text" id="name" required />
      </div>
  
      <div class="d-flex flex-column pa-1">
        <label for="mobile">Phone no</label>
        <input class="pa-2 rounded-sm " placeholder="Enter you mobile number" style="border: 1px solid grey;" v-model="formData.mobile" type="number" id="mobile" required />
      </div>
  
      <div class="d-flex flex-column pa-1">
        <label for="email">Email</label>
        <input class="pa-2 rounded-sm " placeholder="Enter you email" style="border: 1px solid grey;" v-model="formData.email" type="email" id="email" required />
      </div>
  
      <div class="d-flex flex-column">
        <label for="message">Message</label>
        <textarea class="pa-2 rounded-sm " placeholder="Write message..." style="border: 1px solid grey;" v-model="formData.message" id="message" required></textarea>
      </div>
  
      <v-btn type="submit">Send</v-btn>
    </form>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import emailjs from 'emailjs-com'
  
  // Initialize EmailJS
  emailjs.init('uHJ-WtdVaR8tWOzB3') // Replace with your actual EmailJS user ID
  
  const formData = ref({
    name: '',
    mobile: '',
    email: '',
    message: '',
  })
  
  const sendEmail = () => {
    const templateParams = {
      to_name: formData.value.name,
      phone: formData.value.mobile,
      email: formData.value.email,
      message: formData.value.message,
    }
  
    emailjs
      .send('service_qbmje93', 'template_uvc7mbh', templateParams)
      .then(
        (response) => {
          console.log('SUCCESS!', response.status, response.text)
          alert('Sent successfully!')
        },
        (error) => {
          console.error('FAILED...', error)
          alert('Failed to send. Please try again.')
        }
      )
  }
  </script>
  
  <style scoped>
  /* Add your custom styles here */
  </style>
  