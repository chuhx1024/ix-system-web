<template>
    <div class="Xislider-container">
        <a-slider 
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
    options: {
        type: Array,
        default: () => [],
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
.Xislider-container {
    color: purple;
}
</style>
