<template>
    <header class="card-header is-clickable">
        <p class="card-header-title"
            @click="$emit('click')">
            <slot name="title"/>
        </p>
        <slot name="controls"/>
    </header>
</template>

<script>

export default {
    data: () => ({
        isHeader: true,
    }),
};

</script>

<style lang="scss">
    .card-header {
        .card-header-title {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
    }
</style>
