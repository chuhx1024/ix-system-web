<template>
    <div class="index-container">
        <a-form
            :model="modelValue"
            :rules="rules"
            :label-col="{ span: 6 }"
            :wrapper-col="{ span: 12 }"
            ref="formRef"
        >
            <a-form-item
                v-for="item in config.columns" 
                :label="item.label"
                :key="item.label"
                :name="item.prop"
            >
                <component 
                    :is="componentsTypes[item.type]"
                    v-bind="item"
                    v-model="modelValue[item.prop]"
                ></component> 
            </a-form-item>
            <a-form-item :wrapper-col="{ span: 14, offset: 6 }">
                <a-button type="primary" @click="onSubmit" html-type="submit">提交</a-button>
            </a-form-item>
        </a-form>
    </div>
</template>
<script setup lang="ts">
import { markRaw, ref} from 'vue'
import { XiInput, XiTextarea, XiRadio, XiCheckbox, XiSelect, XiSwitch, XiAudio, XiInputNumber, XiSlider  } from './components/index.ts'
const props = defineProps<{
  config: any
  modelValue: any,
  rules: any
}>()

const formRef = ref();

const componentsTypes = markRaw({
    input: XiInput,
    textarea: XiTextarea,
    radio: XiRadio,
    checkbox: XiCheckbox,
    select: XiSelect,
    switch: XiSwitch,
    audio: XiAudio,
    inputNumber: XiInputNumber,
    slider: XiSlider,
})

const onSubmit = () => {
    formRef.value
        .validate()
        .then(() => {
            props.config.searchFn()
        })
        .catch(error => {
            console.log('error', error);
        });
};


</script>
<style lang='less' scoped>
.index-container {
    color: purple;
}
</style>

<!-- 音频处理 https://www.51cto.com/article/763645.html -->
