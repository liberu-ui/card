<template>
    <div class="card-content is-paddingless"
        :style="style">
        <slot/>
    </div>
</template>

<script>
export default {
    name: 'CardContent',

    inject: ['cardState'],

    data: () => ({
        style: {
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
            if (this.cardState.collapsed) {
                this.style.maxHeight = 0;
                this.style.overflowY = 'hidden';
                return;
            }

            this.style.maxHeight = `${this.$el.scrollHeight}px`;

            setTimeout(() => this.style.overflowY = 'visible', 400);
        },
        toggle() {
            const height = this.currentHeight();
            this.update();

            this.$nextTick(() => (this.cardState.resizeParent = this.currentHeight() - height));
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
