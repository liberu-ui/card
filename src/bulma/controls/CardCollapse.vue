<template>
    <card-control @click="toggle()">
        <span class="icon angle"
            :aria-hidden="!expanded">
            <fa icon="angle-down"/>
        </span>
    </card-control>
</template>

<script>

import { library } from '@fortawesome/fontawesome-svg-core';
import { faAngleDown }
    from '@fortawesome/free-solid-svg-icons';
import CardControl from './CardControl.vue';

library.add(faAngleDown);

export default {
    components: { CardControl },

    data: () => ({
        expanded: true,
        isCollapse: true,
    }),

    methods: {
        toggle() {
            this.expanded = !this.expanded;
            this.$emit('toggle');
        },
    },
};

</script>

<style lang="scss">
    .icon.angle[aria-hidden="false"] {
        transform: rotate(180deg);
    }

    .icon.angle {
        transition: transform .300s ease;
    }
</style>
