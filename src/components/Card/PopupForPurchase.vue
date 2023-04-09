<script>
export default {
    inheritAttrs: false,
};
</script>

<script setup>
import { Teleport, Transition, watchEffect, ref } from "vue";
import css from "./PopupForPurchase.module.css";

const TIME_OUT = 1500;

const emit = defineEmits(["close"]);
const props = defineProps(["open", "duration"]);

const timeOut = ref(0);

watchEffect(() => {
    if (props.open === false) return;
    timeOut.value = setTimeout(() => emit("close"), props.duration || TIME_OUT);
});

function closeHandler() {
    clearTimeout(timeOut.value);
    emit("close");
}
</script>

<template>
    <Teleport to="#popup">
        <Transition>

            <div v-if="open" :class="css.popup" role="alert">
                <p :class="css.popup__content">
                    <slot></slot>
                </p>
                <button :class="css.popup__times" @click="closeHandler">&times;</button>
                <div :class="css.popup__line" :style="`animation-duration: ${props.duration || TIME_OUT}ms;`" />
            </div>
            
        </Transition>
    </Teleport>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
    transition: 1000ms;
}

.v-enter-from {
    opacity: 0.2;
    color: red;
    transform: translateY(-100%);
}

.v-leave-to {
    color: red;
    transform: translateX(-500%);
}
</style>
