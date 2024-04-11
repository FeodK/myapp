<script setup>
defineProps({
  totalPrice: Number
})

const emit = defineEmits(['openDrawer'])
</script>

<template>
  <header class="flex flex-col xl:flex-row justify-between border-b border-slate-200 px-10 py-8">
    <RouterLink to="/"
      ><div class="flex items-center justify-center mb-4 xl:mb-0 gap-4">
        <img src="/logo.png" alt="Logo" class="w-10" />
        <div>
          <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
          <p class="text-slate-400">Магазин лучших кроссовок</p>
        </div>
      </div></RouterLink
    >

    <ul class="flex flex-col md:flex-row md:justify-center items-center gap-4 xl:gap-10">
      <li
        @click="() => emit('openDrawer')"
        class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
      >
        <img src="/cart.svg" alt="Cart" />
        <b>{{ totalPrice }} руб.</b>
      </li>

      <RouterLink to="/favorites"
        ><li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black">
          <img src="/heart.svg" alt="" />
          <span>Закладки</span>
        </li></RouterLink
      >

      <li class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black">
        <img src="/profile.svg" alt="Profile" />
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>
