<script setup>
import { ref, computed, watch } from "vue";


    const user = ref({
      name: "John Doe",
      birthdate: "1990-01-01",
      email: "john@example.com",
      description: "A Vue.js enthusiast",
      age: 0,
      profileImage: null,
    });

    const birthYear = computed(() => {
      const birthYear = new Date(user.value.birthdate).getFullYear();

      const birthDate = new Date(user.value.birthdate);
      const today = new Date();
      const age = today.getFullYear() - birthDate.getFullYear();
      user.value.age = age;

      return isNaN(birthYear) ? "Invalid" : birthYear;
    });

    const votingMessage = computed(() => {
      return user.value.age >= 18 ? "Eligible for voting" : "Not eligible for voting";
    });

    const updateProfileImage = (event) => {
      const file = event.target.files[0];
      if (file) {
        // Handle image upload and update user.profileImage
        user.value.profileImage = URL.createObjectURL(file);
      }
    };

    watch(user, (newUser) => {
      const birthDate = new Date(newUser.birthdate);
      const today = new Date();
      const age = today.getFullYear() - birthDate.getFullYear();
      user.value.age = age;
    });

   
 
</script>
<template>
<div class="row">
  <div class="col-md-3"></div>
  <div class="col-md-4">
    <h1>User Details</h1>
    <hr>
    <form>
     
      <div class="row">
      <div class="col-md-6">
        <label for="name">Name</label>
        <input type="text" id="name" v-model="user.name" class="form-control">
      </div>
     
      <div class="col-md-6">
        <label for="birthdate">Birthdate</label>
        <input type="date" id="birthdate" v-model="user.birthdate" class="form-control">
      </div>
     
      <div class="col-md-6">
        <label for="email">Email</label>
        <input type="email" id="email" v-model="user.email" class="form-control">
      </div>
     
      <div class="col-md-6">
        <label for="description">Description</label>
        <textarea id="description" v-model="user.description" class="form-control"></textarea>
      </div>
     
      <div class="col-md-6">
        <label for="profile-image">Profile Image</label>
        <input type="file" id="profile-image" @change="updateProfileImage">
      </div>
       
   
      </div>
    </form>

    <br>
    <hr>
    <h4>Computed Properties </h4>
    <p>Birth Year: {{ birthYear }}</p>
    <p>{{ votingMessage }}</p>
  </div>
  </div>
</template>

