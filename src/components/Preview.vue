<script setup>
const preview = defineModel();
defineProps({
    isValid: Boolean
})
</script>

<template>
    <div class="preview-card">
        <div class="preview-header">
            <h3>Preview</h3>
            <div class="status">
                <!-- recieves prop and reads value in the v-if / else and decides which to show -->
                <span v-if="isValid" class="valid">✓ Valid</span>
                <span v-else class="invalid">✕ Incomplete</span>
            </div>
        </div>

        <div class="preview-content">
            <div class="row">
                <label>Title</label>
                <!-- recieves v-model data -->
                <span>{{ preview.title }}</span>
            </div>

            <div class="row">
                <label>Author</label>
                <span>{{ preview.author }}</span>
            </div>

            <div class="row">
                <label>Type</label>
                <span>{{ preview.type?.join(', ') }}</span>
            </div>

            <div class="row">
                <label>Date Published</label>
                <span>{{ preview.date_published }}</span>
            </div>

            <div class="row description">
                <label>Description</label>
                <span>{{ preview.description }}</span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.preview-card {
    /* fixed size box*/
    width: 100%;
    max-width: 600px;
    height: 680px;
    background: white;
    padding: 36px 40px;
    border-radius: 12px;
    border: 1px solid #e4e7eb;
    box-shadow: 0 6px 24px rgba(0, 0, 0, 0.06);
    font-family: "Segoe UI";
    color: #1f2933;
    overflow-y: auto; /* limits scrolling to inside the box */
}

.preview-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 26px;
}

h3 {
    margin: 0;
    font-size: 22px;
    font-weight: 600;
    letter-spacing: -0.01em;
    color: #102a43;
}

.status span {
    font-size: 14px;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 6px;
}

.valid {
    background: #e6f4ea;
    color: #1b5e20;
}

.invalid {
    background: #fdecea;
    color: #b91c1c;
}

.preview-content {
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.row {
    display: flex;
    flex-direction: column;
    gap: 4px;
    padding-bottom: 12px;
    border-bottom: 1px solid #f0f2f4;
}

.row:last-child {
    border-bottom: none;
}

label {
    font-size: 13px;
    font-weight: 600;
    color: #627d98;
    letter-spacing: 0.04em;
}

span {
    font-size: 15px;
    line-height: 1.5;
    color: #243b53;
}
</style>
