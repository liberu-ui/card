<template>
    <card-control @click="toggle">
        <dropdown-indicator v-model="collapsed"
            @toggle="toggle()"/>
    </card-control>
</template>

<script>

import DropdownIndicator from '@enso-ui/dropdown-indicator';
import CardControl from './CardControl.vue';

export default {
    components: { DropdownIndicator, CardControl },

    data: () => ({
        collapsed: false,
        isCollapse: true,
    }),

    methods: {
        toggle() {
            this.collapsed = !this.collapsed;
            this.$emit('toggle');
        },
    },
};

</script>
