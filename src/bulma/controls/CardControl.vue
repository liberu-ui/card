<template>
    <a class="card-header-icon"
        v-on="$listeners">
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
