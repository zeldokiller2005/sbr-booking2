<template>
  <div class="invite-item">
    <div class="invite-header">
      <span class="invite-title">{{ title }}</span>
    </div>
    
    <div class="invite-pills">
      <div class="pill">{{ time }}</div>
      <div class="pill">{{ person }}</div>
      <div class="pill">{{ role }}</div>
    </div>

    <div class="invite-actions">
      <button class="btn-primary btn-action">Подробнее</button>
      <button class="btn-outline btn-action">Отклонить</button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  time: String,
  person: String,
  role: String
})
</script>

<style scoped>
.invite-item {
  background: #F2F2F2;
  border-radius: 6px;
  padding: 16px;
  margin-bottom: 12px;
  border: 1px solid #e5e5e5;
}

.invite-title { 
  font-size: 15px; 
  font-weight: 500; 
  color: #222; 
  display: block; 
  margin-bottom: 12px; 
}

.invite-pills {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap; 
  gap: 8px; 
  margin-bottom: 14px;
  width: 100%;
}

.pill {
  background-color: #86AEAA;
  color: #ffffff;
  padding: 6px 10px; /* Чуть уменьшили отступы для компактности */
  border-radius: 6px;
  font-size: 12px; 
  font-weight: 500;
  white-space: nowrap;
  flex-shrink: 0; 
}

.invite-actions {
  display: flex;
  gap: 10px;
}

.btn-action {
  padding: 8px 18px;
  font-size: 13px;
  border-radius: 4px;
}

.btn-outline.btn-action {
  background: white;
  border: 1px solid #ddd;
  color: #333;
}
.btn-outline.btn-action:hover {
  background: #f5f5f5;
}
</style>