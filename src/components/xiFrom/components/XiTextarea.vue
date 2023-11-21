<template>
    <div class="XiTextarea-container">
        <a-textarea
            v-model:value="Val"
            placeholder="Autosize height based on content lines"
            :rows="rows"
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
    rows: {
        type: Number,
        default: 4,
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
.XiTextarea-container {
    color: purple;
}
</style>
