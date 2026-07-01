<template>
  <div class="user-card">
    <div class="user-image">
      <img :src="avatar" alt="Avatar" />
      <div class="user-badge" v-if="badge">{{ badge }}</div>
    </div>
    <div class="user-info">
      <h4 class="user-name">{{ name }}</h4>
      <p class="user-bio">{{ bio }}</p>
      <div class="user-actions">
        <button class="btn-primary btn-sm" @click="$emit('invite')">Пригласить</button>
        <button class="btn-outline btn-sm" @click="$emit('details')">Подробнее</button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  name: String,
  bio: String,
  avatar: String,
  badge: String // Добавили проп для бейджика
})
defineEmits(['invite', 'details'])
</script>

<style scoped>
.user-card {
  display: flex;
  background: white;
  border-radius: 6px;
  padding: 16px;
  gap: 16px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.02);
  border: 1px solid #f0f0f0;
}
.user-image {
  width: 100px;
  height: 120px;
  flex-shrink: 0;
  border-radius: 4px;
  overflow: hidden;
  background: #eee;
  position: relative; /* Важно для позиционирования бейджика */
}
.user-image img { width: 100%; height: 100%; object-fit: cover; }

/* Стили для бейджика на фото */
.user-badge {
  position: absolute;
  bottom: 8px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(255, 255, 255, 0.85);
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 11px;
  font-weight: 500;
  white-space: nowrap;
  color: #333;
}

.user-info { display: flex; flex-direction: column; justify-content: space-between; flex: 1; }
.user-name { font-size: 16px; font-weight: 600; margin-bottom: 6px; }
.user-bio { font-size: 13px; color: #666; line-height: 1.4; flex-grow: 1; margin-bottom: 12px; }
.user-actions {
  display: flex;
  gap: 10px;
}
.user-actions .btn-sm { padding: 8px 16px; font-size: 13px; border-radius: 4px; }
.user-actions .btn-primary { color: white; }
</style>