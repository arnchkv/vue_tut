<template>
    <div>
        <h1>Posts</h1>

        <input type="text" name="title" id="title" v-model="title" placeholder="Title" class="title-input">
        <input type="text" name="body" id="body" v-model="body" placeholder="Body" class="body-input">

        <button v-if="isEditing" @click="updatePost">Update</button>
        <button v-if="isEditing" @click="cancelEdit">Cancel</button>

        <button v-else @click="createPost">Create</button>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const posts = ([])

const title = ref('')
const body = ref('')
const post_id = ref(0)
const isEditing = ref(false)
const API_URL = "http://localhost:3000/posts"

const createPost = async () => {
    // console.log(title.value)
    // console.log(body.value)

    const res = await fetch(API_URL, {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            title: title.value,
            body: body.value
        })
    })

    const data = await res.json()

    posts.push(data)
    title.value = ""
    body.value = ""
    post_id.value = 0
}

const updatePost = async () => {
    return true;
}

const cancelEdit = () => {
    return true;
}
</script>


<style scoped>
.title-input {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border: 2px solid #ccc;
    background-color: #f8f8f8;
    color: #111;
    border-radius: 4px;
    resize: vertical;
}

.body-input {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border: 2px solid #ccc;
    background-color: #f8f8f8;
    color: #111;
    border-radius: 4px;
    resize: vertical;
}
</style>