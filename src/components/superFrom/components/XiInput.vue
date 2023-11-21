<template>
    <div class="XiInput-container">
        <a-input
            v-model:value="Val"
        />
    </div>
</template>
<script setup lang="ts">
import { ref, watch } from 'vue'
const emit = defineEmits(["update:modelValue"])


const props = defineProps({
    modelValue: {
        default: () => '',
    },
})
const Val = ref(props.modelValue)
// 监听父组件的值
watch(() => props.modelValue, () => {
    Val.value = props.modelValue
})


// watch(Val, () => {
//     emit("update:modelValue", Val)
// })

// watch(() => Val.value, () => {
//     emit("update:modelValue", Val)
// })

// watchEffect (() => {
//     emit("update:modelValue", Val)
// })


emit("update:modelValue", Val)


</script>
