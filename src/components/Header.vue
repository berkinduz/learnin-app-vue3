<template>
  <Popover>
    <div class="relative pt-6 px-4 sm:px-6 lg:px-8">
      <nav
        class="
          relative
          flex
          items-center
          justify-between
          sm:h-10
          lg:justify-start
        "
        aria-label="Global"
      >
        <div class="flex items-center flex-grow flex-shrink-0 lg:flex-grow-0">
          <div class="flex items-center justify-between w-full md:w-auto">
            <router-link to="/">
              <img
                class="h-8 w-auto sm:h-10"
                src="../../public/assets/mortarboard.png"
              />
            </router-link>
            <div class="-mr-2 flex items-center md:hidden">
              <PopoverButton
                class="
                  bg-white
                  rounded-md
                  p-2
                  inline-flex
                  items-center
                  justify-center
                  text-gray-400
                  hover:text-gray-500 hover:bg-gray-100
                  focus:outline-none
                  focus:ring-2
                  focus:ring-inset
                  focus:ring-indigo-500
                "
              >
                <span class="sr-only">Open main menu</span>
                <MenuIcon class="h-6 w-6" aria-hidden="true" />
              </PopoverButton>
            </div>
          </div>
        </div>
        <div class="hidden md:block md:ml-10 md:pr-4 md:space-x-8">
          <router-link
            v-for="item in navigation"
            :key="item.name"
            :to="item.href"
            class="font-medium text-gray-500 hover:text-gray-900"
            >{{ item.name }}</router-link
          >
        </div>
      </nav>
    </div>

    <transition
      enter-active-class="duration-150 ease-out"
      enter-from-class="opacity-0 scale-95"
      enter-to-class="opacity-100 scale-100"
      leave-active-class="duration-100 ease-in"
      leave-from-class="opacity-100 scale-100"
      leave-to-class="opacity-0 scale-95"
    >
      <PopoverPanel
        focus
        class="
          absolute
          z-10
          top-0
          inset-x-0
          p-2
          transition
          transform
          origin-top-right
          md:hidden
        "
      >
        <div
          class="
            rounded-lg
            shadow-md
            bg-white
            ring-1 ring-black ring-opacity-5
            overflow-hidden
          "
        >
          <div class="px-5 pt-4 flex items-center justify-between">
            <div>
              <img
                class="h-8 w-auto"
                src="https://tailwindui.com/img/logos/workflow-mark-indigo-600.svg"
                alt=""
              />
            </div>
            <div class="-mr-2">
              <PopoverButton
                class="
                  bg-white
                  rounded-md
                  p-2
                  inline-flex
                  items-center
                  justify-center
                  text-gray-400
                  hover:text-gray-500 hover:bg-gray-100
                  focus:outline-none
                  focus:ring-2
                  focus:ring-inset
                  focus:ring-indigo-500
                "
              >
                <span class="sr-only">Close main menu</span>
                <XIcon class="h-6 w-6" aria-hidden="true" />
              </PopoverButton>
            </div>
          </div>
          <div class="px-2 pt-2 pb-3 space-y-1">
            <router-link
              v-for="item in navigation"
              :key="item.name"
              :to="item.href"
              class="
                block
                px-3
                py-2
                rounded-md
                text-base
                font-medium
                text-gray-700
                hover:text-gray-900 hover:bg-gray-50
              "
              >{{ item.name }}</router-link
            >
          </div>
        </div>
      </PopoverPanel>
    </transition>
  </Popover>
</template>


<script>
import { Popover, PopoverButton, PopoverPanel } from "@headlessui/vue";
import { MenuIcon, XIcon } from "@heroicons/vue/outline";

const navigation = [
  { name: "Courses", href: "#" },
  { name: "Categories", href: "#" },
  { name: "Contact", href: "#" },
  { name: "About Us", href: "/about" },
];

export default {
  components: {
    Popover,
    PopoverButton,
    PopoverPanel,
    MenuIcon,
    XIcon,
  },
  setup() {
    return {
      navigation,
    };
  },
};
</script>