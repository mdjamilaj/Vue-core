<template>
    <div class="container">
        <button @click="status = !status">change status</button> <div class="title"> {{ status }} </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            status: false,
        }
    }
}
</script>

<style scoped>
    .title{
        color: blue;
    }
</style>