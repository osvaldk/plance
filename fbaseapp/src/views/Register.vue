<template>
  <div>
    <h1> Create an Account </h1>
    <p> <input type='text' placeholder="Email" v-model='email'/> </p>
    <p> <input type='password' placeholder="Password" v-model='password'/> </p>
    <p> <button @click="register"> Submit </button> </p>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
  import { useRouter } from 'vue-router'
const email = ref('')
const password = ref('')
const router = useRouter() // get a reference to our vue router
const auth = getAuth();
const register = () => { createUserWithEmailAndPassword(auth, email.value, password.value) // need .value because ref()
    .then((data) => {
      console.log('Successfully registered!');
      router.push('/feed') // redirect to the feed
    })
    .catch(error => {
      console.log(error.code)
      alert(error.message);
    });
  }
</script>
