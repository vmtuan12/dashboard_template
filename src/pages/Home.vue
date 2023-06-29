<script setup>
import { ref } from 'vue';
import Modal from '../components/UI/Modal.vue';
import Button from '../components/UI/Button.vue'

const condition = ref(false);

const lasd = () => {
    console.log(123);
};
</script>

<template>
    <div>
        <div class="bg-white rounded-xl shadow flex space-y-4 p-4">
            <Button @click="condition = true">123</Button>
        </div>
        <Modal :condition="condition" @exit-modal="condition = false">123</Modal>
    </div>
</template>

<style scoped>
      
</style>