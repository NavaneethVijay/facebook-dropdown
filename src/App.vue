<template>
  <div id="app">
    <header class="bg-white px-4 py-4 shadow relative">
      <div
        @click="openMenu = !openMenu"
        class="rounded-full inline-block relative"
      >
        <img
          class="inline-block h-10 w-10 rounded-full text-white shadow-solid"
          src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&amp;ixid=eyJhcHBfaWQiOjEyMDd9&amp;auto=format&amp;fit=facearea&amp;facepad=2&amp;w=256&amp;h=256&amp;q=80"
          alt=""
        />
        <div
          class="absolute bottom-0 right-0 h-3 w-3 bg-green-500 rounded-full border-2 border-solid border-white"
        ></div>
      </div>
      <div class="dropdown__main">
        <div
          :class="{
            'transform opacity-100 scale-100 transition ease-in duration-200 submenuOpened': openMenu
          }"
          class="dropdown__wrapper bg-white -mt-2 pt-2 pb-2 rounded-lg px-2 transform opacity-0 scale-50 transition ease-out origin-top-left duration-300 overflow-hidden"
        >
          <transition
            v-if="!isSubmenuOpen"
            name="expand slide-fade"
            @enter="enter"
            @after-enter="afterEnter"
            @leave="leave"
          >
            <div>
              <MenuProfile />
              <div
                class="pt-2 pb-2  px-2 flex items-center rounded-lg hover:bg-gray-200"
              >
                <div class="rounded-full inline-block p-1 icon-button">
                  <svg
                    class="w-6 h-6"
                    fill="currentColor"
                    viewBox="0 0 20 20"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M18 5v8a2 2 0 01-2 2h-5l-5 4v-4H4a2 2 0 01-2-2V5a2 2 0 012-2h12a2 2 0 012 2zM7 8H5v2h2V8zm2 0h2v2H9V8zm6 0h-2v2h2V8z"
                      clip-rule="evenodd"
                    ></path>
                  </svg>
                </div>
                <div class="px-3">
                  <h3 class="font-normal text-md">Give Feedback</h3>
                  <p class="font-light text-gray-700 text-xs">
                    Help us improve the new Facebook.
                  </p>
                </div>
              </div>
              <div>
                <MenuList @submenu="setSubmenu" />
              </div>
            </div>
          </transition>
          <transition
            v-else
            name="expand slide-fade"
            @enter="enter"
            @after-enter="afterEnter"
            @leave="leave"
          >
            <component
              :is="currentSubmenu"
              @closeMenu="isSubmenuOpen = false"
            />
          </transition>
        </div>
      </div>
    </header>
  </div>
</template>
<script>
import MenuList from './components/MenuList.vue'
import MenuProfile from './components/MenuProfile.vue'
import Settings from './components/Menuitems/Settings.vue'
import Privacy from './components/Menuitems/Privacy.vue'
import Display from './components/Menuitems/Display.vue'
export default {
  components: {
    MenuList,
    MenuProfile,
    Settings,
    Privacy,
    Display
  },
  data() {
    return {
      isSubmenuOpen: false,
      openMenu: false,
      prevHeight: 0,
      currentSubmenu: 'Settings'
    }
  },
  methods: {
    setSubmenu(menu) {
      this.isSubmenuOpen = true
      this.currentSubmenu = menu
    },
    showSubmenu() {
      this.isSubmenuOpen = !this.isSubmenuOpen
    },
    enter(element) {
      console.log(element)
      const width = getComputedStyle(element).width
      element.style.width = width
      element.style.height = 'auto'

      const height = getComputedStyle(element).height
      console.log(height)
      this.prevHeight = this.prevHeight != 0 ? this.prevHeight : height
      element.style.width = null
      element.style.height = this.prevHeight

      console.log(height)
      // Force repaint to make sure the
      // animation is triggered correctly.
      getComputedStyle(element).height

      // Trigger the animation.
      // We use `requestAnimationFrame` because we need
      // to make sure the browser has finished
      // painting after setting the `height`
      // to `0` in the line above.
      requestAnimationFrame(() => {
        element.style.height = height
      })
    },
    afterEnter(element) {
      element.style.height = 'auto'
    },
    leave(element) {
      // const height = getComputedStyle(element).height

      element.style.height = this.prevHeight

      // Force repaint to make sure the
      // animation is triggered correctly.
      getComputedStyle(element).height

      requestAnimationFrame(() => {
        element.style.height = this.prevHeight
      })
    }
  }
}
</script>
<style lang="scss">
body {
  background: #f0f2f5;
}
.submenuOpened {
  transform: translateX(0) !important;
}
.icon-button {
  background: #e4e6eb;
}
.dropdown__wrapper {
  padding-bottom: 100%;
  position: absolute;
  top: 100%;
  left: 10px;
  width: 96%;
  z-index: 1;
  box-shadow: 3px 3px 7px 4px #00000012, -3px 2px 5px 0px #00000012;
  overflow: hidden;
}
.expand-enter-active,
.expand-leave-active {
  transition: height 1s ease;
  overflow: hidden;
}

.expand-enter,
.expand-leave-to {
  height: 0;
}
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  position: absolute;
  transition: all 0.3s ease;
  height: 100%;
}
.slide-fade-leave-to {
  height: 0;
  transform: translateX(-100%);
  opacity: 0;
}
.slide-fade-enter
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(40%);
  height: 100%;
  opacity: 0;
}
</style>
