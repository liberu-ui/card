<template>
    <header class="card-header is-clickable"
        :class="{ 'collapsed': cardState.collapsed }">
        <p class="card-header-title"
            @click="toggle">
            <slot name="title"/>
        </p>
        <slot name="controls"/>
    </header>
</template>

<script>
export default {
    name: 'CardHeader',

    inject: ['cardState', 'toggle'],
};
</script>

<style lang="scss">
    .card-header {
        border-top-left-radius: inherit;
        border-top-right-radius: inherit;

        &.collapsed {
            border-bottom-left-radius: inherit;
            border-bottom-right-radius: inherit;
        }

        .card-header-title {
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
    }
</style>
