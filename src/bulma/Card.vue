<template>
    <div class="card animated"
        v-if="!leaving">
        <slot/>
        <loader size="medium"
            v-if="loading"/>
    </div>
</template>

<script>

import Loader from '@enso-ui/loader/bulma';

export default {
    components: { Loader },

    props: {
        loading: {
            type: Boolean,
            default: false,
        },
        collapsed: {
            type: Boolean,
            default: false,
        },
    },

    data: () => ({
        leaving: false,
    }),

    computed: {
        header() {
            return this.$children.find(comp => comp.isHeader);
        },
        collapse() {
            return !!this.header && this.header.$children.find(comp => comp.isCollapse);
        },
        content() {
            return this.$children.find(comp => comp.isContent);
        },
        remove() {
            return !!this.header && this.header.$children.find(comp => comp.isRemove);
        },
    },

    mounted() {
        if (!!this.collapse && !!this.content) {
            this.content.collapsed = this.collapsed;
            this.collapse.collapsed = this.collapsed;
            this.header.$on('click', this.collapse.toggle);
            this.collapse.$on('toggle', this.content.toggle);
        }

        this.content.$on('resize', size => this.$emit('resize', size));

        if (this.remove) {
            this.remove.$on('remove', () => (this.leaving = true));
        }
    },

    methods: {
        resize(size) {
            this.content.resize(size);
        },
        destroy() {
            this.$emit('remove');
            this.$el.parentNode.removeChild(this.$el);
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

            .card-header {
                border-top-left-radius: 0.5em;
                border-top-right-radius: 0.5em;
            }
        }
    }
</style>
