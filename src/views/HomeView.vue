<script setup lang="ts">
import ListItem from '@/components/ListItem.vue'
import type { LegoFlowerDto } from '@/types/legoFlower'
import { onMounted } from 'vue'
import axios from 'axios'

//const flowerList = [
//  {name: "sunflower", number_of_pieces: 200, difficulty: "hard"},
//  {name: "tulip", number_of_pieces: 100, difficulty: "medium"},
//  {name: "primrose", number_of_pieces: 50, difficulty: "easy"}
//] as LegoFlowerDto[]

const flowerList = [] as LegoFlowerDto

const flowerImages = {
  sunflower: "@assets/imgs/sunflower-square.png",
  tulip: "@assets/imgs/tulip-square.png",
  primrose: "@assets/imgs/primrose-square.png"
}

function loadData(): void {
  axios
      .get<LegoFlowerDto[]>('http://localhost:8080/legoFlowers')
      .then((response) => {
        flowerList.push(response.data)
        console.log("backend data: " + response.data)
      })
      .catch((error) => console.log("error: " + error))

  //const endpoint = 'http://localhost:8080/legoFlowers'
  //const requestOptions = {
  //  method: 'GET',
  //  redirect: 'follow'
  //}
  //fetch(endpoint, requestOptions)
  //    .then(response => response.json())
  //    .then(result => result.forEach(flower => {
  //      this.flowerList.push(flower)
  //    }))
  //  .catch( error =>  console.log("error: " + error.error))

  console.log("flowerlist: " + flowerList)
}

onMounted(() =>
  loadData()
)


</script>

<template>
  <main>
    <div v-for="flower of flowerList" :key="flower.name">
      <ListItem :lego-flower-name="flower.name" :lego-flower-img="flowerImages.tulip" />
    </div>
  </main>
</template>
