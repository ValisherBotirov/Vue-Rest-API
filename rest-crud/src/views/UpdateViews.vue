<template>
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

    <button @click="updateUser">Submit</button>
  </form>
</template>

<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const id = route.params.id

const name = ref(route.query.name)
const cost = ref(route.query.cost)
const adress = ref(route.query.address)

const updateUser = (e) => {
  e.preventDefault()

  const obj = {
    product_type_id: 0,
    id,
    name_uz: name.value,
    cost: cost.value,
    address: adress.value,
    created_date: new Date()
  }

  axios
    .put(`http://94.158.54.194:9092/api/product`, obj)
    .then((res) => {
      console.log(res)
    })
    .catch((err) => {
      console.log(err)
    })
}
</script>
