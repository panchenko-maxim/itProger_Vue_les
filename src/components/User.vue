<template>
    <div className="user">
        <button @click="deleteUser(index)">Delete</button>
        <h3>{{ user.name }}</h3>
        <p>{{ user.email }} - <b>{{ user.pass }}</b></p>
    </div>
</template>

<script>
export default {
    props: {
        user: {
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        },
        deleteUser: {
            type: Function,
            required: true
        }
    }
}
</script>

<style scoped>
.user {
    border: 1px solid black;
}

button {
    border: 1px solid yellow;
}
</style>