<template>
    <div class="index-container">
        <div >
        </div>
        <a-form
            :model="modelValue"
        >
            <a-form-item
                :label="item.label"
                v-for="item in config.columns" 
                :key="item.label"
                :name="item.prop"
            >
                <a-input
                    v-if="item.type === 'input'"
                    :value="modelValue[item.prop]"
                    @input="handleModel($event.target.value, item.prop)"
                />
                <a-radio-group  
                    v-if="item.type === 'radio'"  
                    :value="modelValue[item.prop]" 
                    @input="handleModel($event.target.value, item.prop)"
                >
                    <a-radio v-for="option in item.options" :key="option.value"  :value="option.value">{{option.label}}</a-radio>
                </a-radio-group>
                <a-select
                    v-if="item.type === 'select'"  
                    :value="modelValue[item.prop]" 
                    @select="handleModel($event, item.prop)"
                >
                    <a-select-option v-for="option in item.options" :key="option.value"  :value="option.value">{{option.label}}</a-select-option>
                </a-select>
                <a-switch 
                    v-if="item.type === 'switch'"
                    :checked="modelValue[item.prop]" 
                    @change="handleModel($event, item.prop)"
                />
            </a-form-item>
            <a-form-item>
                <a-button type="primary" @click="config.searchFn()" html-type="submit">提交</a-button>
            </a-form-item>
        </a-form>
    </div>
</template>
<script setup lang="ts">
const props = defineProps<{
  config: any
  modelValue: any
}>()
const emit = defineEmits(['update:modelValue'])

const handleModel = (val, arr) => {
    // eslint-disable-next-line vue/no-mutating-props
    props.modelValue[arr] = val
    emit('update:modelValue', props.modelValue)
}
</script>
<style lang='less' scoped>
.index-container {
    color: purple;
}
</style>
