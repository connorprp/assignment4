<script setup>

import { defineModel, ref } from 'vue'

const title = defineModel('title')
const author = defineModel('author')
const type = defineModel('type', { default: () => [] })
const date_published = defineModel('date_published')
const description = defineModel('description')

const emit = defineEmits(['isValid'])

const invalidFields = ref([])

function validate() {
    invalidFields.value = []

    if (!title.value) invalidFields.value.push('title')
    if (!author.value) invalidFields.value.push('author')
    if (!type.value?.length) invalidFields.value.push('type')
    if (!date_published.value) invalidFields.value.push('date_published')
    if (!description.value) invalidFields.value.push('description')

    if (invalidFields.value.length === 0) {
        emit('isValid', true)
    } else {
        emit('isValid', false)
    }
}
</script>

<template>
    <div class="page">
        <div class="form-card">
            <h1>Book Record</h1>

            <div class="field">
                <label for="title">Title</label>
                <input id="title" v-model="title">
                <p v-if="invalidFields.includes('title')" class="error">Required</p>
            </div>

            <div class="field">
                <label for="author">Author</label>
                <input id="author" v-model="author">
                <p v-if="invalidFields.includes('author')" class="error">Required</p>
            </div>

            <div class="field">
                <label for="type">Type</label>
                <select id="type" v-model="type" multiple>
                    <option disabled value=""></option>
                    <option value="Fiction">Fiction</option>
                    <option value="Non-fiction">Non-fiction</option>
                    <option value="Sci-fi">Sci-fi</option>
                </select>
                <p v-if="invalidFields.includes('type')" class="error">Required</p>
            </div>

            <div class="field">
                <label for="date-published">Date Published</label>
                <input id="date-published" type="date" v-model="date_published">
                <p v-if="invalidFields.includes('date_published')" class="error">Required</p>
            </div>

            <div class="field">
                <label for="description">Description</label>
                <textarea id="description" v-model="description"></textarea>
                <p v-if="invalidFields.includes('description')" class="error">Required</p>
            </div>

            <div id="button-container">
                <button @click="validate">Validate</button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.page {
    background: #f5f6f7;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    font-family: "Segoe UI";
    color: #1f2933;
}

.form-card {
    height: 680px;
    width: 100%;
    max-width: 640px;
    background: white;
    padding: 36px 40px;
    border-radius: 12px;
    box-shadow: 0 6px 24px rgba(0, 0, 0, 0.06);
    border: 1px solid #e4e7eb;
    overflow-y: auto;
}

h1 {
    margin: 0 0 28px;
    font-size: 22px;
    font-weight: 600;
    letter-spacing: -0.02em;
    color: #102a43;
}

.field {
    display: flex;
    flex-direction: column;
    margin-bottom: 22px;
}

label {
    font-size: 14px;
    font-weight: 600;
    margin-bottom: 6px;
    color: #334e68;
}

input,
select,
textarea {
    padding: 10px 12px;
    font-size: 15px;
    border-radius: 6px;
    border: 1px solid #cbd2d9;
    background: #fff;
    transition: border 0.15s ease, box-shadow 0.15s ease;
}

textarea {
    min-height: 110px;
    resize: vertical;
}

input:focus,
select:focus,
textarea:focus {
    outline: none;
    border-color: #486581;
    box-shadow: 0 0 0 2px rgba(72, 101, 129, 0.15);
}

.error {
    margin-top: 4px;
    font-size: 13px;
    color: #b91c1c;
}


#button-container {
    display: flex;
    justify-content: flex-end;
    margin-top: 10px;
}

button {
    background: #334e68;
    color: white;
    border: none;
    padding: 10px 18px;
    font-size: 15px;
    font-weight: 600;
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.15s ease, transform 0.05s ease;
}

button:hover {
    background: #243b53;
}

button:active {
    transform: translateY(1px);
}
</style>
