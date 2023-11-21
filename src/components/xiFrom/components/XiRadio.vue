<template>
    <div class="XiRadio-container">
        <a-radio-group  
            v-model:value="Val"
        >
            <a-radio v-for="option in options" :key="option.value"  :value="option.value">{{option.label}}</a-radio>
        </a-radio-group>
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
