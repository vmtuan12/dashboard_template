<script setup>
import { computed, onBeforeMount, onMounted, onUnmounted, ref, watch } from 'vue';
import Navbar from '../components/UI/Navbar.vue';
import ProfileDropdown from '../components/UI/ProfileDropdown.vue'

const smallBar = ref(false)

const main = ref()
const scrollPosition = ref(0)

const handleScroll = () => {
    scrollPosition.value = main.value.scrollTop
}

window.addEventListener('scroll', handleScroll)

onBeforeMount(() => {
    if(window.innerWidth <= 640) {
        smallBar.value = true
    }
});

onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
    <div class="flex w-full h-full">
        <Navbar @handle-bar-size="smallBar = !smallBar" :smallbar="smallBar" />
        <div 
            ref="main"
            class="sticky top-0 z-0 min-h-screen transition-all duration-500 ease-in-out  sm:px-4 pb-4 overflow-x-hidden max-h-screen"
            :class="smallBar ? 'px-2 sm:px-8 w-[calc(100%-64px)]' : 'w-0 sm:px-8 sm:w-[calc(100%-300px)]'"
            @scroll="handleScroll"
        >
            <div 
                class="sticky z-0 w-full top-0 flex items-center justify-between py-3 rounded-b-3xl transition-all duration-500 ease-in-out"
                :class="scrollPosition > 0 ? 'bg-[#52a1f5] text-white px-5' : 'text-[#52a1f5]'"
            >
                <p class="text-lg font-semibold">Dashboard</p>
                <ProfileDropdown />
            </div>
            <div class="">
                <router-view></router-view>
            </div>
        </div>
    </div>
</template>