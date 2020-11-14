<template>
  <div>
    <header class="flex items-center px-2 py-2 mb-2">
      <div class="p-1 hover:bg-gray-200 rounded-full">
        <svg
          @click="$emit('closeMenu')"
          class="w-6 h-6"
          fill="currentColor"
          viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            d="M7.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l2.293 2.293a1 1 0 010 1.414z"
            clip-rule="evenodd"
          ></path>
        </svg>
      </div>
      <div class="pl-4">
        <h3 class="font-bold text-2xl">
          Settings & Privacy
        </h3>
      </div>
    </header>
    <ul>
      <li
        v-for="(item, index) in 4"
        :key="index"
        class="flex items-center justify-between py-2 hover:bg-gray-200 rounded-lg px-2"
      >
        <div class="flex items-center">
          <div class="rounded-full inline-block p-1 icon-button">
            <svg
              class="w-6 h-6"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"
              ></path>
            </svg>
          </div>
          <div class="px-3">
            <h3 class="font-normal text-md">Display Preferences</h3>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>
