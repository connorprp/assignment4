<script setup>
import Form from './components/Form.vue';
import Preview from './components/Preview.vue';
import Record from './models/Record.js';

import { ref } from 'vue';

const preview = ref(new Record()); //uses js class to create ref
const formIsValid = ref(false); //toggleable value, defaults to false and changes from toggleCheck

function toggleCheck(result) { //run when emit is recieved from Form child, result is data/arg from emit
  formIsValid.value = result; 
}

</script>

<template>
  <div id="app">
    <div class="app-page">
      <div class="layout">
        <!-- recieves emit isValid, runs toggleCheck
         registers v-model for all fields from Form -->
        <Form @isValid="toggleCheck" v-model:title="preview.title" v-model:author="preview.author"
          v-model:type="preview.type" v-model:date_published="preview.date_published"
          v-model:description="preview.description" />
          <!-- sends v-model to other child, don't need to specify all fields
           also passed prop formIsValid to child to handle check mark -->
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
