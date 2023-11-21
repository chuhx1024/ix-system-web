

<template>
    <div>
        <super-from
            v-model=formData
            :config="config"
            :rules="rules"
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
    name1: 1234,
    name2: 1234,
    name3: '1',
    name4: ['1', '2'],
    name5: '1',
    name6: true,
    name7: 5,
    name8: '',
    name9: 5,
    // name10: 5,
})
const rules: Record<string, Rule[]> = {
    name1: [
        { required: true, message: 'name1不能为空', trigger: 'change' },
        { min: 3, max: 9, message: '长度为 3 to 9', trigger: 'blur' },
    ],
    name2: [{ required: true, message: 'name2不能为空', trigger: 'change' }],
    name3: [{ required: true, message: 'name2不能为空', trigger: 'change' }],
};

const config = reactive( {
    columns: [
        {type: 'input', label: '输入框1', prop: 'name1'},
        {type: 'textarea', label: '输入框2', prop: 'name2', rows: 3},
        {type: 'radio', label: '输入框3', prop: 'name3', options: [{ value: '1', label: '选项一'}, { value: '2', label: '选项二'}]},
        {type: 'checkbox', label: '输入框4', prop: 'name4', options: [{ value: '1', label: '选项一'}, { value: '2', label: '选项二'}]},
        {type: 'select', label: '输入框5', prop: 'name5', options: [{ value: '1', label: '选项一'}, { value: '2', label: '选项二'}]},
        {type: 'switch', label: '输入框6', prop: 'name6'},
        {type: 'inputNumber', label: '输入框7', prop: 'name7', max: 12, min: 2},
        {type: 'audio', label: '输入框8', prop: 'name8'},
        {type: 'slider', label: '输入框9', prop: 'name9'},
        // {type: 'rate', label: '输入框10', prop: 'name10'},
    ],
    searchFn: () => {
        console.log(formData.value)
    },
})


</script>

