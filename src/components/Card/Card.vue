<script setup>
import { ref } from "vue";
import style from "./Card.module.css";
import Popup from "./PopupForPurchase.vue";

const quantity = ref(5000);
const isOpen = ref(false);
</script>

<template>
    <div>
        <button @click="isOpen=true, quantity--">
            <slot :quantity="quantity">Bum</slot>
        </button>
        <Popup :open="isOpen" @close="isOpen = false">The car was bought.</Popup>
    </div>
</template>