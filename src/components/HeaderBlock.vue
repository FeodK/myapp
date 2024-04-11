<script setup>
import { ref } from 'vue'


defineProps({
  totalPrice: Number,
});

const emit = defineEmits(["openDrawer",]);

const menuOpen = ref(false)

const closeMenu = () => {
  menuOpen.value = false
}

const openMenu = () => {
  menuOpen.value = true
}

</script>

<template>
  <header
    class="flex md:flex-col xl:flex-row justify-between border-b border-slate-200 px-10 py-8"
  >
    <RouterLink to="/myapp/"
      ><div class="flex items-center justify-center mb-4 xl:mb-0 gap-4">
        <img src="/logo.png" alt="Logo" class="w-10" />
        <div>
          <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
          <p class="text-slate-400">Магазин лучших кроссовок</p>
        </div>
      </div></RouterLink
    >

    <ul 
      class=" hidden md:flex mdflex-col lg:flex-row md:justify-center items-center gap-4 xl:gap-10"
    >
      <li
        @click="() => emit('openDrawer')"
        class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
      >
        <img src="/cart.svg" alt="Cart" />
        <b>{{ totalPrice }} руб.</b>
      </li>

      <RouterLink to="/myapp/favorites"
        ><li
          class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
        >
          <img src="/heart.svg" alt="" />
          <span>Закладки</span>
        </li></RouterLink
      >

      <li
        class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
      >
        <img src="/profile.svg" alt="Profile" />
        <span>Профиль</span>
      </li>

    </ul>

    <ul v-if="menuOpen"
      class="fixed top-0 left-0 overflow-hidden bg-white h-screen w-full z-10 flex flex-col justify-center items-center gap-10"
    >
      <li
        @click="() => emit('openDrawer')"
        class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
      >
        <img src="/cart.svg" alt="Cart" />
        <b>{{ totalPrice }} руб.</b>
      </li>

      <RouterLink to="/myapp/favorites"
        ><li
          class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
        >
          <img src="/heart.svg" alt="" />
          <span>Закладки</span>
        </li></RouterLink
      >

      <li
        class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
      >
        <img src="/profile.svg" alt="Profile" />
        <span>Профиль</span>
      </li>

      <li @click="closeMenu" class="md:hidden cursor-pointer">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M6 18 18 6M6 6l12 12"
          />
        </svg>
      </li>
    </ul>
    <button @click="openMenu" class="md:hidden">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
        />
      </svg>
    </button>
  </header>
</template>
