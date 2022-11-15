<template>
    <div class="dialog" v-if="show" @click.stop="hideDialog">
        <div @click.stop class="dialog__content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'app-dialog',
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideDialog() {
            this.$emit('update:show', false)
        }
    }
}
</script>

<style scoped>
.dialog {
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(139, 180, 201, 0.7);
    position: fixed;
    display: flex;
}
.dialog__content {
    margin: auto;
}

@media screen and (max-width: 767px) {
    .dialog__content {
    margin: 125px 0 0;
} 
}
</style>