<template>
    <card-control @click="cardState.collapsed = !cardState.collapsed">
        <dropdown-indicator :open="!cardState.collapsed"/>
    </card-control>
</template>

<script>

import DropdownIndicator from '@enso-ui/dropdown-indicator';
import CardControl from './CardControl.vue';

export default {
    name: 'CardCollapse',

    components: { DropdownIndicator, CardControl },

    inject: ['cardState'],
};

</script>
