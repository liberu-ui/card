<template>
    <a class="card-header-icon is-naked">
        <slot/>
    </a>
</template>

<script>
export default {
    name: 'CardControl',
};
</script>

<style lang="scss">
    .card-header-icon {
        padding: 0.75rem 0.75rem 0.75rem 0;
    }
</style>
