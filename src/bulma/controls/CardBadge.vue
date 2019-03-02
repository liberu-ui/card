<template>
    <card-control>
        <span :class="['tag', type]">
            {{ label }}
        </span>
    </card-control>
</template>

<script>
import CardControl from './CardControl.vue';

export default {
    name: 'CardBadge',

    components: { CardControl },

    props: {
        label: {
            type: String,
            required: true,
        },
        type: {
            type: String,
            default: null,
        },
    },
};
</script>
