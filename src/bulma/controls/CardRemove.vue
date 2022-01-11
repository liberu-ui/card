<template>
    <card-control @click="cardState.removed = true">
        <a class="delete is-small"/>
    </card-control>
</template>

<script>
import CardControl from './CardControl.vue';

export default {
    name: 'CardRemove',

    components: { CardControl },

    inject: ['cardState'],
};
</script>
