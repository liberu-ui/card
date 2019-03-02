<template>
    <div class="card-content is-paddingless"
        :style="contentStyle">
        <slot/>
    </div>
</template>

<script>
export default {
    name: 'CardContent',

    inject: ['cardState'],

    data: () => ({
        contentStyle: {
            overflowY: 'hidden',
            maxHeight: 0,
        },
    }),

    watch: {
        'cardState.collapsed': 'toggle',
        'cardState.resizeSelf': 'resize',
    },

    mounted() {
        this.update();
    },

    methods: {
        update() {
            this.contentStyle.maxHeight = this.cardState.collapsed
                ? 0
                : `${this.$el.scrollHeight}px`;
        },
        toggle() {
            const height = this.currentHeight();
            this.update();

            this.$nextTick(() => (this.cardState.resizeParent =                this.currentHeight() - height));
        },
        resize(delta) {
            if (delta === null) {
                return;
            }

            this.$el.style.maxHeight = `${this.currentHeight() + delta}px`;
            this.$nextTick(() => (this.cardState.resizeParent = delta));

            this.cardState.resizeSelf = null;
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
