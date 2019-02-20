<template>
    <div class="card-content is-paddingless"
        :style="computedStyle">
        <slot/>
    </div>
</template>

<script>

export default {
    data: () => ({
        ready: false,
        collapsed: false,
        isContent: true,
    }),

    computed: {
        maxHeight() {
            if (this.collapsed) {
                return { maxHeight: 0 };
            }

            return this.ready
                ? { maxHeight: `${this.$el.scrollHeight}px` }
                : {};
        },
        overflowY() {
            return { 'overflow-y': 'hidden' };
        },
        computedStyle() {
            return Object.assign({}, this.maxHeight, this.overflowY);
        },
    },

    mounted() {
        this.$nextTick(() => {
            this.init();
        });
    },

    methods: {
        init() {
            if (!this.collapsed) {
                this.$el.style.maxHeight = this.$el.scrollHeight;
            }
            setTimeout(() => {
                this.ready = true;
            }, 100);
        },
        toggle() {
            const maxHeight = this.currentHeight();
            this.collapsed = !this.collapsed;
            this.$nextTick(() => this
                .$emit('resize', this.currentHeight() - maxHeight));
        },
        resize(size) {
            const maxHeight = this.currentHeight();
            this.$el.style.maxHeight = `${maxHeight + size}px`;
        },
        currentHeight() {
            return parseInt(this.$el.style.maxHeight, 10);
        },
    },
};

</script>

<style>
    .card-content.is-paddingless {
        transition: max-height .400s ease;
    }
</style>
