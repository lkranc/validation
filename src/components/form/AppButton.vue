<template>
    <button
        class="app-button"
        :type="type"
        @click.prevent="$emit('click')"
        :disabled="asyncLoader || disabled"
    >
        <slot></slot>
        <span v-if="asyncLoader">
            loader...
        </span>
    </button>
</template>

<script>
export default {
    name: "AppButton",
    data: () => ({}),
    props: {
        type: {
            type: String,
            default: 'button'
        },
        disabled: {
            type: Boolean,
            default: false
        },
        asyncLoader: {
            type: Boolean,
            default: false
        },
    },
    methods: {}
}
</script>

<style scoped lang="scss">
.app-button {
}
</style>