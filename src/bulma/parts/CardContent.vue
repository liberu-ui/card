<template>
    <div class="card-content"
        v-if="!cardState.collapsed">
        <slot/>
    </div>
</template>

<script>
export default {
    name: 'CardContent',

    inject: ['cardState'],
};
</script>
