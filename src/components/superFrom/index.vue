<template>
    <div class="index-container">
        <div >
        </div>
        <a-form>
            <a-form-item
                :label="item.label"
                v-for="item in config" 
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
                    <a-radio value="1">Sponsor</a-radio>
                    <a-radio value="2">Venue</a-radio>
                </a-radio-group>
            </a-form-item>
        </a-form>
        {{modelValue}}
    </div>
</template>
<script setup lang="ts">
const props = defineProps<{
  config: any
  modelValue: any
}>()
const emit = defineEmits(['update:modelValue'])

const handleModel = (id, arr) => {
    // eslint-disable-next-line vue/no-mutating-props
    props.modelValue[arr] = id
    emit('update:modelValue', props.modelValue)
}
</script>
<style lang='less' scoped>
.index-container {
    color: purple;
}
</style>
