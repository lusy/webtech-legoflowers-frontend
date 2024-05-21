<script setup lang="ts">

const props = defineProps({
  legoFlowerName : {
    type: String,
    required: true
  },
  legoFlowerImage: {
    type: String,
    required: false
  }
})

</script>

<template>
  <div class="listItem">
    <img :src="legoFlowerImage" :alt="legoFlowerName"/>
    {{ legoFlowerImage }}
    {{ legoFlowerName }}
  </div>
</template>

<style scoped lang="scss">
.listItem {
  border: 1px solid black;
}
</style>
