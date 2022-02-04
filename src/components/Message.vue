<template>
    <div class="message-container">
        <p>{{msg}}</p>
    </div>
</template>

<script>
export default {
    name:'Message',
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container {
        color: #004085;
        background-color: #CCE5FF;
        border:  2px solid #B8DAFF;
        border-radius: 5px;
        width: 300px;
        margin: 0 auto;
        margin-bottom: 20px;
    }
</style>