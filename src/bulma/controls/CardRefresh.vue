<template>
    <card-control @click="$emit('refresh')">
        <span class="icon is-small">
            <fa icon="sync"/>
        </span>
    </card-control>
</template>

<script>
import { FontAwesomeIcon as Fa } from '@fortawesome/vue-fontawesome';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSync }
    from '@fortawesome/free-solid-svg-icons';
import CardControl from './CardControl.vue';

library.add(faSync);

export default {
    name: 'CardRefresh',

    components: { Fa, CardControl },
};

</script>
