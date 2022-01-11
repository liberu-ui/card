<template>
    <div class="card"
        v-if="!cardState.removed">
        <slot/>
        <loader size="medium"
            v-if="loading"/>
    </div>
</template>

<script>
import Loader from '@enso-ui/loader/bulma';

export default {
    name: 'Card',

    components: { Loader },

    provide() {
        return {
            cardState: this.cardState,
            toggle: this.toggle,
        };
    },

    props: {
        collapsed: {
            type: Boolean,
            default: false,
        },
        collapsible: {
            type: Boolean,
            default: false,
        },
        loading: {
            type: Boolean,
            default: false,
        },
    },

    emits: ['collapse', 'expand', 'remove'],

    data: v => ({
        cardState: {
            collapsed: v.collapsed,
            collapsible: v.collapsible,
            removed: false,
        },
    }),

    watch: {
        collapsed(collapsed) {
            this.cardState.collapsed = collapsed;
            this.$emit(collapsed ? 'collapse' : 'expand');
        },
        'cardState.removed': 'remove',
    },

    methods: {
        toggle() {
            if (this.cardState.collapsible) {
                this.cardState.collapsed = !this.cardState.collapsed;
            }
        },
        remove() {
            this.$emit('remove');
        },
    },
};
</script>

<style lang="scss">
    .card {
        position: relative;

        &.is-rounded {
            border-radius: 0.5em;
        }
    }
</style>
