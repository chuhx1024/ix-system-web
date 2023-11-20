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

                <a-checkbox-group 
                    v-if="item.type === 'checkbox'" 
                    :value="modelValue[item.prop]" 
                    @input="handleCheckbox($event.target.value, item.prop)"
                >
                    <a-row>
                        <a-col :span="8">
                            <a-checkbox v-for="option in item.options" :key="option.value"  :value="option.value">{{option.label}}</a-checkbox>
                        </a-col>
                    </a-row>
                </a-checkbox-group>
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
                <a-input-number 
                    v-if="item.type === 'inputNumber'"
                    :value="modelValue[item.prop]"
                    @change="handleModel($event, item.prop)"
                    :min="item.min" 
                    :max="item.max" 
                />
                <div  v-if="item.type === 'audio'">
                    <div v-if="isBlank">
                        <audio  id="audio"  controls autoplay></audio>
                        <a-space>
                            <a-button type="primary" @click="startAudio" size="small">开始</a-button>
                            <a-button  @click="stopAudio(item.prop)" size="small">结束</a-button>
                        </a-space>
                    </div>
                    <div v-else>
                        <audio :src="url" :value="modelValue[item.prop]"  controls ></audio>
                        <a-button type="primary" @click="resetAudio(item.prop)" size="small">重置</a-button>
                    </div>
                </div>

            </a-form-item>
            <a-form-item :wrapper-col="{ span: 14, offset: 6 }">
                <a-button type="primary" @click="config.searchFn()" html-type="submit">提交</a-button>
            </a-form-item>
        </a-form>
    </div>
</template>
<script setup lang="ts">
import {ref} from 'vue'
const props = defineProps<{
  config: any
  modelValue: any
}>()
const emit = defineEmits(['update:modelValue'])

let recorder = ''
let audioChunks = []
let blob = ''
let url = ref({})
let isBlank = ref(true)

const handleModel = (val, arr) => {
    props.modelValue[arr] = val
    emit('update:modelValue', props.modelValue)
}
const handleCheckbox = (val, arr) => {
    if (props.modelValue[arr].includes(val)) {
        props.modelValue[arr] = props.modelValue[arr].filter(item => item !== val)
    } else {
        props.modelValue[arr].push(val)
    }
    emit('update:modelValue', props.modelValue)
}

const startAudio = () => {
    let videoTarget = document.getElementById('audio');
    navigator.mediaDevices.getUserMedia({audio: true, video: false})
        .then((stream) => {
            recorder = new MediaRecorder(stream);
            videoTarget.srcObject = stream;
            videoTarget = (...arg) => {
                console.log(arg);
            }
            recorder.ondataavailable = (event) => {
                url.value = URL.createObjectURL(event.data);
                console.log(url)
                let link = document.createElement("a");
                link.target = "_blank";
                link.href = url;
                // link.click();
                audioChunks.push(event.data);

            }
            recorder.start();
        });
}
const resetAudio = (attr) => {
    isBlank.value = true
    props.modelValue[attr] = ''
    emit('update:modelValue', props.modelValue)
}

const stopAudio = (attr) => {
    recorder.stop();
    blob = new Blob(audioChunks, {
        type: 'audio/mp3', 
    })
    isBlank.value = false
    console.log(blob)
    // 向外传递值
    props.modelValue[attr] = blob
    emit('update:modelValue', props.modelValue)

}
</script>
<style lang='less' scoped>
.index-container {
    color: purple;
}
</style>

<!-- 音频处理 https://www.51cto.com/article/763645.html -->
