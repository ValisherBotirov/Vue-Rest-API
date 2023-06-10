<template>
  <div class="about">
    <form action="">
      <div>
        <label for="">Name</label>
        <input type="text" v-model="name" />
      </div>
      <div>
        <label for="">Cost</label>
        <input type="number" v-model="cost" />
      </div>
      <div>
        <label for="">Adress</label>
        <input type="text" v-model="adress" />
      </div>

      <button @click="createUser">Submit</button>
    </form>
  </div>
</template>

<script setup>
import axios from 'axios'
import { ref } from 'vue'

const name = ref('')
const cost = ref(null)
const adress = ref('')

function createUser(e) {
  e.preventDefault()

  const obj = {
    product_type_id: 0,
    name_uz: name.value,
    cost: cost.value,
    address: adress.value,
    created_date: new Date()
  }
  axios
    .post('http://94.158.54.194:9092/api/product', obj)
    .then((res) => {
      console.log(res)
    })
    .catch((err) => {
      console.log(err)
    })
}
</script>
