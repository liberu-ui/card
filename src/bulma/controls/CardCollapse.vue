<template>
    <card-control @click="toggle">
        <dropdown-indicator :open="!cardState.collapsed"/>
    </card-control>
</template>

<script>

import DropdownIndicator from '@enso-ui/dropdown-indicator';
import CardControl from './CardControl.vue';

export default {
    name: 'CardCollapse',

    components: { DropdownIndicator, CardControl },

    inject: ['cardState', 'toggle'],
};

</script>
