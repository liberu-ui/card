<template>
    <card-control @click="$emit('remove')">
        <a class="delete is-small"/>
    </card-control>
</template>

<script>
import CardControl from './CardControl.vue';

export default {
    components: { CardControl },

    data: () => ({
        isRemove: true,
    }),
};
</script>
