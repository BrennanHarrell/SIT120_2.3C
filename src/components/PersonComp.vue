<script setup>
import NewComp from "./NewComp.vue";

const props = defineProps({
    text: {
        type: String,
        required: true,
    }

});

const emit = defineEmits(['emitCheck'])

</script>

<template>

    <div>
        <button @click="$emit('emitCheck')">{{ text }}</button>
    </div>
    <NewComp>
    <template #Caption>
        Image not loading
    </template>
    </NewComp>



</template>

