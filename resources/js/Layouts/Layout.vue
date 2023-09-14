<script setup>
    import MainNav from '@/Components/MainNav.vue'
    import { ref } from 'vue';
    import { Link } from '@inertiajs/vue3';

    let width = ref('w-[250px]')
    let hide = ref(false)

    function toggleWidth() {
        if(width.value == 'w-[250px]') {
            width.value = 'w-[100px]'
            hide.value = true
        }else {
            width.value = ['w-[250px]']
            hide.value = false
        }
    }
</script>

<template>

<div class="flex min-h-screen">
    <div id="sidebar" class="p-6 duration-500 bg-sky-900" :class="width" style="position: relative;">
        <button class="text-xl text-white" @click="toggleWidth" style="position: absolute; right: 10px; top:10px">
            <i class="fa-solid fa-bars"></i>
        </button>
        <div id="branding" :hidden="hide">
            <img src="Kristine.png" alt="User Logo"
                class="w-[170px] h-[170px] mx-auto rounded-full object-cover">
            <h1 class="my-6 text-3xl text-center text-white">{{ $page.props.auth.user.name }}</h1>

        </div>



        <div class="mt-10">
            <MainNav :hidden="hide"></MainNav>
        </div>
    </div>
    <div id="container" class="flex-1">
        <slot />
    </div>
</div>

</template>
