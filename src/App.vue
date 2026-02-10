<script setup>
import Form from './components/Form.vue';
import Preview from './components/Preview.vue';
import Record from './models/Record.js';

import { ref } from 'vue';

const preview = ref(new Record());
const formIsValid = ref(false);

function toggleCheck(result) {
  formIsValid.value = result.valid ?? result;
}

</script>

<template>
  <div id="app">
    <div class="app-page">
      <div class="layout">
        <Form @isValid="toggleCheck" v-model:title="preview.title" v-model:author="preview.author"
          v-model:type="preview.type" v-model:date_published="preview.date_published"
          v-model:description="preview.description" />
        <Preview v-model="preview" :is-valid="formIsValid" />
      </div>
    </div>
  </div>


</template>

<style scoped>
.app-page {
  background: #f5f6f7;
  padding: 60px 40px;
}

.layout {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 32px;
  align-items: start;
}
</style>
