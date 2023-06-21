<script>
export default {
    name: 'Cat',
    props: ['cat', 'active']
}
</script>

<template>
    <span class="cat-name" @click="$emit('set-cat', cat)" :class="{ 'inactive': active && active.name !== cat.name }">{{ cat.name }}</span>
</template>

<style scoped>
    .cat-name {
        font-size: 1.25em;
        font-weight: bold;
        float: left;
    }

    .cat-name + .cat-name {
        margin-left: 2rem;
    }
</style>