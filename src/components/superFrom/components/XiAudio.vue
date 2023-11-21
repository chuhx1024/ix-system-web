<template>
    <div class="XiAudio-container">
        <div v-if="isBlank">
            <audio  id="audio"  controls autoplay></audio>
            <a-space>
                <a-button type="primary" @click="startAudio" size="small">开始</a-button>
                <a-button  @click="stopAudio()" size="small">结束</a-button>
            </a-space>
        </div>
        <div v-else>
            <audio :src="url"  controls ></audio>
            <a-button type="primary" @click="resetAudio()" size="small">重置</a-button>
            <a-input
                class="XiAudio-hidden-input"
                disabled
                v-model:value="Val"
            />
        </div>
    </div>
</template>
<script setup lang="ts">
import {ref} from 'vue'

const emit = defineEmits(['update:modelValue'])

const props = defineProps({
    modelValue: {
        default: () => '',
    },
})
const Val = ref(props.modelValue)

let recorder = ''
let audioChunks = []
let blob = ''
let url = ref({})
let isBlank = ref(true)

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
const resetAudio = () => {
    isBlank.value = true
    Val.value = ''
    emit('update:modelValue', Val)
}

const stopAudio = () => {
    recorder.stop();
    blob = new Blob(audioChunks, {
        type: 'audio/mp3', 
    })
    isBlank.value = false
    // 向外传递值
    Val.value = blob
    emit('update:modelValue', Val)

}
</script>
<style lang='less' scoped>
.XiAudio-container {
    .XiAudio-hidden-input {
        width: 0;
        height: 0;
        opacity: 0;
        pointer-events: none;
    }
}
</style>
