<template>
    <div class="index-container">
        <div >
        </div>
        <a-form
            :model="modelValue"
            :label-col="{ span: 6 }"
            :wrapper-col="{ span: 12 }"
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
                <a-button type="primary" @click="config.searchFn()" html-type="submit">提交</a-button>
            </a-form-item>
        </a-form>
    </div>
</template>
<script setup lang="ts">
import { markRaw} from 'vue'
import { XiInput, XiRadio, XiCheckbox, XiSelect, XiSwitch, XiAudio, XiInputNumber } from './components/index.ts'
defineProps<{
  config: any
  modelValue: any
}>()
// const emit = defineEmits(['update:modelValue'])

// let recorder = ''
// let audioChunks = []
// let blob = ''
// let url = ref({})
// let isBlank = ref(true)

const componentsTypes = markRaw({
    input: XiInput,
    radio: XiRadio,
    checkbox: XiCheckbox,
    select: XiSelect,
    switch: XiSwitch,
    audio: XiAudio,
    inputNumber: XiInputNumber,
})

// const handleModel = (val, arr) => {
//     props.modelValue[arr] = val
//     emit('update:modelValue', props.modelValue)
// }
// const handleCheckbox = (val, arr) => {
//     if (props.modelValue[arr].includes(val)) {
//         props.modelValue[arr] = props.modelValue[arr].filter(item => item !== val)
//     } else {
//         props.modelValue[arr].push(val)
//     }
//     emit('update:modelValue', props.modelValue)
// }

// const startAudio = () => {
//     let videoTarget = document.getElementById('audio');
//     navigator.mediaDevices.getUserMedia({audio: true, video: false})
//         .then((stream) => {
//             recorder = new MediaRecorder(stream);
//             videoTarget.srcObject = stream;
//             videoTarget = (...arg) => {
//                 console.log(arg);
//             }
//             recorder.ondataavailable = (event) => {
//                 url.value = URL.createObjectURL(event.data);
//                 console.log(url)
//                 let link = document.createElement("a");
//                 link.target = "_blank";
//                 link.href = url;
//                 // link.click();
//                 audioChunks.push(event.data);

//             }
//             recorder.start();
//         });
// }
// const resetAudio = (attr) => {
//     isBlank.value = true
//     props.modelValue[attr] = ''
//     emit('update:modelValue', props.modelValue)
// }

// const stopAudio = (attr) => {
//     recorder.stop();
//     blob = new Blob(audioChunks, {
//         type: 'audio/mp3', 
//     })
//     isBlank.value = false
//     console.log(blob)
//     // 向外传递值
//     props.modelValue[attr] = blob
//     emit('update:modelValue', props.modelValue)

// }
</script>
<style lang='less' scoped>
.index-container {
    color: purple;
}
</style>

<!-- 音频处理 https://www.51cto.com/article/763645.html -->
