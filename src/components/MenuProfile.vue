<template>
  <div>
    <header
      class="flex items-center pt-4 pb-4 rounded-lg hover:bg-gray-200 px-2"
    >
      <div class="relative">
        <img
          class="inline-block h-12 w-12 rounded-full text-white shadow-solid"
          src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&amp;ixid=eyJhcHBfaWQiOjEyMDd9&amp;auto=format&amp;fit=facearea&amp;facepad=2&amp;w=256&amp;h=256&amp;q=80"
          alt=""
        />
        <div
          class="absolute bottom-0 right-0 h-3 w-3  bg-green-500 rounded-full border-2 border-solid border-white"
        ></div>
      </div>
      <div class="px-3">
        <h3 class="font-bold text-xl">Navaneeth Vijay</h3>
        <p class="font-light text-gray-700 text-xs">See your profile</p>
      </div>
    </header>
    <div class="border-b my-2"></div>
  </div>
</template>
<script>
export default {
  name: 'MenuProfile'
}
</script>
