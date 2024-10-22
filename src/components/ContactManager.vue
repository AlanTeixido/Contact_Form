<template>
  <div>
    <form @submit.prevent="submitContact">
      <input v-model="contactName" type="text" placeholder="Nombre" required />
      <input v-model="contactPhone" type="tel" placeholder="Número de Teléfono" required />
      <button type="submit">Agregar Contacto</button>
    </form>

    <ul>
      <li v-for="contact in contacts" :key="contact.phone">
        {{ contact.name }} -
        <a v-bind:href="'tel:' + contact.phone">{{ contact.phone }}</a>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps({
  contacts: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['addContact'])

const contactName = ref('')
const contactPhone = ref('')

const submitContact = () => {
  if (contactName.value && contactPhone.value) {
    const newContact = {
      name: contactName.value,
      phone: contactPhone.value
    }
    emit('addContact', newContact) 
    contactName.value = ''
    contactPhone.value = ''
  }
}
</script>

<style scoped>
form {
  margin-bottom: 20px;
}

input {
  margin: 5px;
}

button {
  margin-top: 10px;
}

ul {
  list-style-type: none;
  padding: 0;
}
</style>
