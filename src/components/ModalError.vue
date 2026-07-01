<template>
  <div class="modal-overlay" @click.self="$emit('close')">
    <div class="modal-content error-modal">
      <h2 class="error-title">Ошибка</h2>
      <p class="error-msg">Неверный запрос. Обратитесь в техподдержку</p>
      <button class="btn-primary btn-full" @click="$emit('close')">Принять</button>
    </div>
  </div>
</template>

<script setup>
defineEmits(['close'])
</script>

<style scoped>
.error-modal { text-align: center; max-width: 400px; padding: 40px; }
.error-title { font-size: 28px; font-weight: 500; margin-bottom: 16px; }
.error-msg { color: #444; margin-bottom: 30px; font-size: 16px; }
.btn-full {
  width: 100%;
  padding: 14px;
  border-radius: 6px;
  font-size: 16px;
}
</style>