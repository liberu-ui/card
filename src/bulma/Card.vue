<template>
    <div class="card">
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

    data: v => ({
        cardState: {
            collapsed: v.collapsed,
            collapsible: v.collapsible,
            remove: false,
        },
    }),

    provide() {
        return {
            cardState: this.cardState,
            toggle: this.toggle,
        };
    },

    watch: {
        collapsed(collapsed) {
            this.cardState.collapsed = collapsed;
            this.$emit(collapsed ? 'collapse' : 'expand');
        },
        'cardState.remove': 'remove',
    },

    methods: {
        toggle() {
            if (this.cardState.collapsible) {
                this.cardState.collapsed = !this.cardState.collapsed;
            }
        },
        remove() {
            this.$el.parentNode.removeChild(this.$el);
            this.$emit('remove');
            this.$destroy();
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
