<template>
    <div class="card-content"
        v-show="cardState.collapsible ? !cardState.collapsed : true">
        <slot/>
    </div>
</template>

<script>
export default {
    name: 'CardContent',

    inject: ['cardState'],
};
</script>
