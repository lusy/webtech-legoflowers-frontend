<script setup lang="ts">
import ListItem from '@/components/ListItem.vue'
import type { LegoFlowerDto } from '@/types/legoFlower'
import { onMounted, ref, type Ref } from 'vue'
import axios from 'axios'

const flowerList : Ref<LegoFlowerDto[]> = ref([])

const flowerImages = {
  sunflower: "@assets/imgs/sunflower-square.png",
  tulip: "@assets/imgs/tulip-square.png",
  primrose: "@assets/imgs/primrose-square.png"
}

const baseUrl = import.meta.env.VITE_APP_BACKEND_BASE_URL

function loadData(): void {
  axios
      .get<LegoFlowerDto[]>(`${baseUrl}/legoFlowers`)
      .then((response) => {
        flowerList.value = response.data
      })
      .catch((error) => console.log("error: " + error))
}

onMounted(() => loadData())


</script>

<template>
  <main>
    <div v-for="flower of flowerList" :key="flower.name">
      <ListItem :lego-flower-name="flower.name" :lego-flower-img="flowerImages.tulip" />
    </div>
  </main>
</template>
