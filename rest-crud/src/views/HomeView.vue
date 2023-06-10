<template>
  <div>
    <!-- <pre>{{ data }}</pre> -->
    <ol>
      <li v-for="(item, index) in data" :key="index" class="item" @click="passUpdatePage(item?.id)">
        {{ item?.name_uz }}

        <span @click="deleteItem(item?.id)" style="margin-left: 40px">D</span>
      </li>
    </ol>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const router = useRouter()

const data = ref([])

function fetchData() {
  axios
    .get('http://94.158.54.194:9092/api/product')
    .then((res) => {
      data.value = res.data
    })
    .catch((err) => {
      console.log(err)
    })
}

function deleteItem(id) {
  console.log(id, 'id')
  axios
    .delete(`http://94.158.54.194:9092/api/product/${id}`)
    .then((res) => {
      console.log(res)
      fetchData()
    })
    .catch((err) => {
      console.log(err)
    })
}

function passUpdatePage(id) {
  const singleData = data.value.find((el) => el.id === id)
  router.push({
    path: `update/${id}`,
    query: {
      name: singleData?.name_uz,
      cost: singleData?.cost,
      address: singleData?.address
    }
  })
}

onMounted(() => {
  fetchData()
})
</script>

<style>
.item {
  cursor: pointer;
}
</style>
