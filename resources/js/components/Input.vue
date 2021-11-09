<template>
        <div class="input-group">
            <input :value="value" :type ="type" v-on:input="$emit('input', $event.target.value)" class="form-control" placeholder="hello add a task, bye">
        </div>
</template>

<script>

export default {
    props: ['type', 'value'],

}
</script>
