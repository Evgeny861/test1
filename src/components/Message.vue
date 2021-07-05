<template>
    <div class="message">
        <p>{{ message }}</p>
    </div>
</template>

<script>
export default {
    props: {
        message: {
            type: String,
            required: true
        }
    }
}
</script>

<style scoped>

.message {
    text-align: center;
    padding: 20px;

}

p {
    color: rgb(247, 8, 8);
}
</style>