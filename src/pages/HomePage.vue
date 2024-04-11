<script setup>
import CardList from '../components/CardList.vue'
import axios from 'axios'
import debounce from 'lodash.debounce'
import { inject, reactive, watch, ref, onMounted, provide} from 'vue'

const { cart, addToCart, removeFromCart } = inject('cart')

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuerry: ''
})

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuerry) {
      params.title = `*${filters.searchQuerry}*`
    }

    const { data } = await axios.get(`https://3bba161d5bcbdd3d.mokky.dev/items`, {
      params
    })
    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      isAdded: false
    }))
  } catch (error) {
    console.log(error)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://3bba161d5bcbdd3d.mokky.dev/favorites`)
    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.item_id === item.id)

      if (!favorite) {
        return item
      }

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id
      }
    })
  } catch (error) {
    console.log(error)
  }
}


const onChangeSelect = (event) => {
  filters.sortBy = event.target.value

}

const onChangeSearchInput = debounce((event) => {
  filters.searchQuerry = event.target.value
}, 500)

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      const obj = {
        item_id: item.id
      }
      item.isFavorite = true

      const { data } = await axios.post(`https://3bba161d5bcbdd3d.mokky.dev/favorites`, obj)

      item.favoriteId = data.id
    } else {
      item.isFavorite = false
      await axios.delete(`https://3bba161d5bcbdd3d.mokky.dev/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }
  } catch (error) {
    console.log(error)
  }
}

const onClickAddPlus = (item) => {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
}

watch(filters, fetchItems)

watch(cart, () => {
  items.value = items.value.map((item) => ({
    ...item,
    isAdded: false
  }))
})

provide('items', {
  items,
  addToFavorite,
})

onMounted(async () => {
  const localCart = localStorage.getItem('cart')
  cart.value = localCart ? JSON.parse(localCart) : []

  await fetchItems()
  await fetchFavorites()

  items.value = items.value.map((item) => ({
    ...item,
    isAdded: cart.value.some((cartItem) => cartItem.id === item.id)
  }))
})
</script>

<template>
  <div class="flex flex-col lg:flex-row lg:justify-between items-center">
    <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

    <div class="flex flex-col sm:flex-row gap-4">
      <select @change="onChangeSelect" class="py-2 px-3 bg-white border rounded-md otline-none">
        <option value="name">По названию</option>
        <option value="price">По цене (дешевле)</option>
        <option value="-price">По цене (дорогие)</option>
      </select>
      <div class="relative">
        <img class="absolute left-4 top-3" src="/search.svg" alt="" />
        <input
          @input="onChangeSearchInput"
          class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
          type="text"
          placeholder="Поиск..."
        />
      </div>
    </div>
  </div>

  <div class="mt-10">
    <CardList :items="items" @add-to-favorite="addToFavorite" @add-to-cart="onClickAddPlus" />
  </div>
</template>
