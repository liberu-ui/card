<template>
    <div class="card-content is-paddingless">
        <slot v-if="!cardState.collapsed"/>
    </div>
</template>

<script>
export default {
    name: 'CardContent',

    inject: ['cardState'],
};
</script>
