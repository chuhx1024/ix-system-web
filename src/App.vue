

<template>
    <div>
        <super-from
            v-model=formData
            :config="config"
        >
        </super-from>
    </div>
    {{formData}}
    <div>
    </div>
    {{config}}
</template>

<script setup lang="ts">
import SuperFrom from './components/superFrom/index.vue'
import { ref, reactive} from 'vue'
const formData = ref({
    name1: 12345,
    name2: 1234,
    name3: '1',
    name4: '1',
    name5: true,
})

const config = reactive( {
    columns: [
        {type: 'input', label: '输入框1', prop: 'name1'},
        {type: 'input', label: '输入框2', prop: 'name2'},
        {type: 'radio', label: '输入框3', prop: 'name3', options: [{ value: '1', label: '选项一'}, { value: '2', label: '选项二'}]},
        {type: 'select', label: '输入框4', prop: 'name4', options: [{ value: '1', label: '选项一'}, { value: '2', label: '选项二'}]},
        {type: 'switch', label: '输入框5', prop: 'name5'},
    ],
    searchFn: () => {
        console.log(formData.value)
    },
})

</script>

<style scoped>


</style>
