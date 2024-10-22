<template>
  <div class="container">
    <h1>Libreta de Contactos</h1>
    
    <input class="search-bar" v-model="searchQuery" placeholder="Buscar por nombre" />

    <ContactManager :contacts="filteredContacts" @add-contact="addContact" />
  </div>
</template>


<script setup>
import { ref, computed } from 'vue'
import ContactManager from './components/ContactManager.vue'

const contacts = ref([])

const searchQuery = ref('')

const filteredContacts = computed(() => {
  return contacts.value.filter(contact =>
    contact.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})

const addContact = (newContact) => {
  contacts.value.push(newContact)
}
</script>

<style scoped>
h1 {
  font-family: Arial, sans-serif;
}

input {
  margin: 10px 0;
}
</style>
