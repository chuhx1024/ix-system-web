

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
})

const config = reactive([
    {type: 'input', label: '输入框1', prop: 'name1'},
    {type: 'input', label: '输入框2', prop: 'name2'},
    {type: 'radio', label: '输入框3', prop: 'name3'},
])

</script>

<style scoped>


</style>
