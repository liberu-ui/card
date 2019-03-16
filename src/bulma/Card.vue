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

    inject: {
        parentCardState: {
            from: 'cardState',
            default: {
                resizeSelf: null,
                resizeParent: null,
            },
        },
    },

    props: {
        loading: {
            type: Boolean,
            default: false,
        },
        collapsed: {
            type: Boolean,
            default: false,
        },
        transition: {
            type: Boolean,
            default: false,
        },
    },

    data: v => ({
        cardState: {
            collapsed: v.collapsed,
            removing: false,
            resizeSelf: null,
            resizeParent: null,
        },
    }),

    provide() {
        return {
            cardState: this.cardState,
        };
    },

    watch: {
        collapsed(collapsed) {
            this.cardState.collapsed = collapsed;
        },
        'cardState.removing': 'destroy',
        'cardState.collapsed': 'toggle',
        'cardState.resizeParent': 'resizeParent',
    },

    methods: {
        collapse() {
            this.toggle(false);
        },
        expand() {
            this.toggle(true);
        },
        toggle(collapsed) {
            this.$emit(collapsed ? 'collapse' : 'expand');
        },
        resizeParent(delta) {
            if (delta === null) {
                return;
            }

            this.$nextTick(() => (this.parentCardState.resizeSelf = delta));

            this.cardState.resizeParent = null;
        },
        destroy() {
            if (!this.transition) {
                this.$nextTick(() => this.$el.parentNode.removeChild(this.$el));
                this.$destroy();
                this.$emit('remove');
            }
        },
    },
};
</script>

<style lang="scss">
    .card {
        position: relative;

        &.is-rounded {
            border-radius: 0.5em;

            .card-header {
                border-top-left-radius: 0.5em;
                border-top-right-radius: 0.5em;
            }
        }
    }
</style>
