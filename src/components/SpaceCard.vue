<template>
  <div class="space-card">
    <div class="space-image-wrapper" :style="{ backgroundImage: `url(${image})` }">
      <div class="image-actions">
        <span class="action-badge">Фото</span>
        <span class="action-badge">Информация</span>
      </div>
      <div class="space-title">{{ title }}</div>
    </div>

    <div class="time-grid">
      <!-- Верхний ряд -->
      <div v-for="time in timeSlots.slice(0, 6)" :key="time" 
           class="time-slot" :class="{ 'active': selectedSlots.includes(time) }"
           @click="toggleSlot(time)">{{ time }}</div>
      
      <button class="btn-primary block-btn" @click="$emit('book')">Забронировать</button>

      <!-- Нижний ряд -->
      <div v-for="time in timeSlots.slice(6, 12)" :key="time" 
           class="time-slot" :class="{ 'active': selectedSlots.includes(time) }"
           @click="toggleSlot(time)">{{ time }}</div>
      
      <button class="btn-outline block-btn" @click="$emit('more')">Подробнее</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  title: String,
  image: String
})
defineEmits(['book', 'more'])

const timeSlots = [
  '08:00 - 09:00', '09:00 - 10:00', '10:00 - 11:00', '11:00 - 12:00', '12:00 - 13:00', '13:00 - 14:00',
  '14:00 - 15:00', '15:00 - 16:00', '16:00 - 17:00', '17:00 - 18:00', '18:00 - 19:00', '19:00 - 20:00'
]

const selectedSlots = ref([])

const toggleSlot = (slot) => {
  if (selectedSlots.value.includes(slot)) {
    selectedSlots.value = selectedSlots.value.filter(s => s !== slot)
  } else {
    selectedSlots.value.push(slot)
  }
}
</script>

<style scoped>
.space-card {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.04);
  border: 1px solid #f0f0f0;
}
.space-image-wrapper {
  position: relative;
  height: 180px;
  background-color: #ccc;
  background-size: cover;
  background-position: center;
}
.image-actions {
  position: absolute;
  top: 16px;
  left: 16px;
  display: flex;
  gap: 10px;
}
.action-badge {
  background: white;
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 13px;
  font-weight: 500;
}
.space-title {
  position: absolute;
  bottom: 16px;
  left: 16px;
  background: white;
  padding: 6px 14px;
  border-radius: 4px;
  font-weight: 500;
  font-size: 15px;
}
.time-grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr) 130px;
  gap: 8px;
  padding: 16px;
  background: #fafafa;
}
.time-slot {
  background: var(--color-pill-bg);
  color: var(--color-pill-text);
  padding: 10px 0;
  text-align: center;
  border-radius: 4px;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}
.time-slot:hover { background: #dbeae5; }

/* ИЗМЕНЕНИЕ: Цвет активного слота меняем на #86AEAA */
.time-slot.active {
  background: #86AEAA;
  color: white;
}

.block-btn {
  padding: 0;
  border-radius: 4px;
  font-size: 13px;
  font-weight: 500;
  width: 100%;
  height: 38px;
}
.btn-outline.block-btn { background: white; border: 1px solid #ddd; }
</style>