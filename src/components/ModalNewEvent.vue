<template>
  <div class="modal-overlay" @click.self="$emit('close')">
    <div class="modal-content">
      <h2 class="modal-title">Новое мероприятие</h2>

      <div class="form-group">
        <label>Название</label>
        <input type="text" placeholder="Введите название мероприятия" class="input-underline" />
      </div>

      <div class="form-group">
        <label>Выберите время мероприятия</label>
        <div class="time-picker-grid">
          <div 
            v-for="slot in timeSlots" 
            :key="slot" 
            class="time-pill" 
            :class="{ 'selected': selectedSlots.includes(slot) }"
            @click="toggleSlot(slot)"
          >
            {{ slot }}
          </div>
        </div>
      </div>

      <div class="form-group">
        <label>Ответственные лица</label>
        <div class="chips-container">
          <div class="chip">Иван Иванов</div>
          <div class="chip">Елена Иванова</div>
          <div class="chip-add">+</div>
        </div>
      </div>

      <div class="form-group">
        <label>Дополнительная информация</label>
        <input type="text" placeholder="Добавить комментарий" class="input-underline" />
      </div>

      <div class="modal-footer">
        <button class="btn-primary btn-block" @click="$emit('submit')">Забронировать</button>
        <button class="btn-outline btn-block" @click="$emit('close')">Отмена</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const timeSlots = [
  '08:00 - 09:00', '09:00 - 10:00', '10:00 - 11:00',
  '11:00 - 12:00', '12:00 - 13:00', '13:00 - 14:00',
  '14:00 - 15:00', '15:00 - 16:00', '16:00 - 17:00',
  '17:00 - 18:00', '18:00 - 19:00', '19:00 - 20:00'
]

const selectedSlots = ref([])

const toggleSlot = (slot) => {
  if (selectedSlots.value.includes(slot)) {
    selectedSlots.value = selectedSlots.value.filter(s => s !== slot)
  } else {
    selectedSlots.value.push(slot)
  }
}

defineEmits(['close', 'submit'])
</script>

<style scoped>
.modal-title { font-size: 24px; font-weight: 500; margin-bottom: 24px; }
.form-group { margin-bottom: 24px; }
.form-group label { display: block; font-size: 14px; color: #444; margin-bottom: 12px; }
.input-underline {
  width: 100%;
  border: none;
  border-bottom: 1px solid #ccc;
  padding: 8px 0;
  font-size: 15px;
  color: #888;
  background: transparent;
}
.input-underline:focus { border-bottom-color: var(--color-primary); }

.time-picker-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
}
.time-pill {
  background: var(--color-pill-bg);
  color: var(--color-pill-text);
  text-align: center;
  padding: 12px 0;
  border-radius: 6px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.2s;
}
.time-pill:hover { background: #dbeae5; }

/* ИЗМЕНЕНИЕ 1: Выбранное время становится #86AEAA */
.time-pill.selected {
  background: #86AEAA;
  color: white;
}

.chips-container { 
  display: flex; 
  gap: 10px; 
  align-items: center; 
  border-bottom: 1px solid #ccc; 
  padding-bottom: 10px; 
  width: 100%; 
}

/* ИЗМЕНЕНИЕ 2: Чипсы становятся #86AEAA */
.chip {
  background: #86AEAA;
  color: white;
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 14px;
}
.chip-add {
  background: transparent;
  font-size: 24px;
  cursor: pointer;
  color: #666;
  line-height: 1;
}

.modal-footer {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 12px;
  margin-top: 32px;
}
.btn-block { padding: 14px; border-radius: 6px; font-size: 16px; width: 100%; }
.btn-outline.btn-block { background: white; border: 1px solid #eee; font-weight: 500; }
</style>