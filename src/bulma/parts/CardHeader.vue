<template>
    <header class="card-header is-clickable">
        <p class="card-header-title"
            @click="cardState.collapsed = !cardState.collapsed">
            <slot name="title"/>
        </p>
        <slot name="controls"/>
    </header>
</template>

<script>

export default {
    name: 'CardHeader',

    inject: ['cardState'],
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
