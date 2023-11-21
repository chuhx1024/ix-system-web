<template>
    <div class="XiInputNumber-container">
        <a-input-number 
            v-model:value="Val"
            :min="min" 
            :max="max" 
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
    max: {
        type: Number,
        default: 1000,
    },
    min: {
        type: Number,
        default: 0,
    },
})
const Val = ref(props.modelValue)
// 监听父组件的值
watch(() => props.modelValue, () => {
    Val.value = props.modelValue
})



emit("update:modelValue", Val)
</script>
<style lang='less' scoped>
.XiInputNumber-container {
    color: purple;
}
</style>
