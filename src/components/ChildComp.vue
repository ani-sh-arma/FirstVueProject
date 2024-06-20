<script setup>
    const props = defineProps({
        msg: String
    })

    const emit = defineEmits(['response'])
    emit('response', 'Response Message from Child')
</script>

<template>
    <h1>{{ msg || 'No props passed yet' }}</h1>
    <slot>Fallback Content</slot>
</template>