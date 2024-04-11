<script setup>
import { ref } from "vue";

defineProps({
  totalPrice: Number,
});

const emit = defineEmits(["openDrawer"]);

const menuOpen = ref(false);

const closeMenu = () => {
  menuOpen.value = false;
};

const openMenu = () => {
  menuOpen.value = true;
};
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
      class="hidden md:flex mdflex-col lg:flex-row md:justify-center items-center gap-4 xl:gap-10"
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

    <div v-if="menuOpen" class="fixed top-0 left-0 overflow-hidden bg-white h-screen w-full z-10 ">
      <div class="flex items-center gap-5 mb-8 p-6">
        <svg
          @click="closeMenu"
          class="opacity-30 cursor-pointer rotate-180 transition hover:opacity-100 hover:-translate-x-1"
          width="16"
          height="14"
          viewBox="0 0 16 14"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M1 7H14.7143"
            stroke="black"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
          <path
            d="M8.71436 1L14.7144 7L8.71436 13"
            stroke="black"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
        <h2 class="text-2xl font-bold">Меню</h2>
      </div>

      <ul
        class="flex flex-col gap-10 p-6"
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
            @click="closeMenu"
            class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
          >
            <img src="/heart.svg" alt="" />
            <span>Закладки</span>
          </li></RouterLink
        >
        <li
          @click="closeMenu"
          class="flex items-center gap-3 cursor-pointer text-gray-500 hover:text-black"
        >
          <img src="/profile.svg" alt="Profile" />
          <span>Профиль</span>
        </li>
      </ul>
    </div>
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
