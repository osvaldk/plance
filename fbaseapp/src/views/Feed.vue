<template>
    <div>
        <h1> Feed </h1>
        <h3> This page is for users only </h3>
    </div>
</template>

<script setup>
import { getAuth, onAuthStateChanged} from 'firebase/auth'
import { useRouter } from 'vue-router'
import { onBeforeUnmount } from 'vue'
const router = useRouter()
const auth = getAuth()
const authListener = onAuthStateChanged(auth, function(user) {
    if (!user) { // not logged in
        alert('you must be logged in to view this. redirecting to the home page')
        router.push('/')
    }
})
onBeforeUnmount(() => {
    authListener()
})
  
</script>