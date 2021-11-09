<template>
        <button v-bind:type="type" class="input-group-text" id="addon-wrapping">{{ value }}</button>
</template>

<script>

export default {
    props: {
        type: String,
        value: String
    }
}
</script>
