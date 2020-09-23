<template>
    <div class="input-text__wrapper">
        <label class="input-text__label">
            <span
                v-if="label"
                class="input-text__label--text"
            >
                {{ label }}
            </span>
            <input
                :type="type"
                :value="value"
                @keyup.prevent="handleInput"
                @blur="$emit('blur')"
                class="input-text__input"
                :class="{ error }"
            >
        </label>
    </div>
</template>

<script>
export default {
    name: "InputText",
    data: () => ({}),
    props: {
        type: {
            type: String,
            default: 'text'
        },
        value: {
            type: String,
            default: ''
        },
        label: {
            type: String,
            default: ''
        },
        error: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        handleInput({ target: input }) {
            this.$emit('update:value', input.value)
        }
    }
}
</script>

<style scoped lang="scss">
    .input-text {
        &__wrapper {}
        &__label {
            &--text { min-width: 100px; }
        }
        &__input {
            outline: none;
            border: 1px solid gray;
            margin-bottom: 10px;
            &:focus {
                border: 1px solid blue;
            }
            &.error {
                border: 1px solid red;
            }
        }
    }
</style>