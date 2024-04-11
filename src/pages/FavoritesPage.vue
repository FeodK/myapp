<script setup>
import { onMounted, ref, computed } from 'vue'
import axios from 'axios'

import CardList from '../components/CardList.vue'
import InfoBlock from '../components/InfoBlock.vue'

const favorites = ref([])
const isFavoritesEmpty = computed(() => favorites.value.length === 0)


onMounted(async () => {
  try {
    const { data } = await axios.get(
      `https://3bba161d5bcbdd3d.mokky.dev/favorites?_relations=items`
    )

    favorites.value = data.map((obj) => obj.item)
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
    <div v-if="isFavoritesEmpty" class="flex h-screen justify-center items-center">
      <InfoBlock
        title="Закладок нет :("
        description="Вы ничего не добавили в закладки."
        image-url="emoji-1.png"
      />
    </div>
    <div v-else>
        <h2 class="text-3xl font-bold mb-8">Мои закладки</h2>
        <CardList :items="favorites" is-favorites />
    </div>
</template>
