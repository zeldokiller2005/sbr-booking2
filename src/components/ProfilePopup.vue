<template>
  <div class="profile-popup">
    <div class="popup-arrow"></div>
    
    <div class="popup-inner">
      <div class="popup-header">
        <div class="user-info">
          <div class="user-name">Иван Иванов</div>
          <div class="user-email">example@yandex.ru</div>
        </div>
        
        <!-- Вместо крестика теперь отображается ваша иконка шестеренки -->
        <img :src="settingsIcon" class="settings-icon" alt="Настройки" />
      </div>
      
      <div class="popup-footer">
        <button class="btn-logout" @click="handleLogout">Выход</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineEmits } from 'vue'
// Убедитесь, что имя файла совпадает с тем, что вы положили в assets
import settingsIcon from '../assets/settings.png' 

const emit = defineEmits(['close'])
const handleLogout = () => { emit('close') }
</script>

<style scoped>
.profile-popup {
  position: absolute;
  top: 50px;
  right: 0;
  width: 200px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.15);
  z-index: 1000;
}

/* Треугольная стрелочка сверху */
.popup-arrow {
  position: absolute;
  top: -8px;
  right: 14px;
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 8px solid white;
}

.popup-inner { display: flex; flex-direction: column; }

/* Изменено: flex + justify-content: space-between, чтобы имя было слева, а иконка справа */
.popup-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 16px 16px 12px 16px;
}

.user-info { display: flex; flex-direction: column; gap: 2px; }
.user-name { font-size: 14px; font-weight: 600; color: #1a1a1a; }
.user-email { font-size: 12px; color: #777; }

/* Стили для маленькой иконки шестеренки */
.settings-icon {
  width: 14px;
  height: 14px;
  object-fit: contain;
  cursor: pointer;
  margin-top: 2px; /* Небольшая коррекция, чтобы быть на уровне имени */
  /* Если ваша картинка цветная, а нужна черная, раскомментируйте строку ниже: */
  /* filter: brightness(0) saturate(100%) invert(0); */
}

.popup-footer { padding: 0 16px 16px 16px; }

.btn-logout {
  width: 100%;
  background: var(--color-primary);
  color: white;
  border: none;
  border-radius: 6px;
  padding: 10px 0;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s;
}
.btn-logout:hover { background: var(--color-primary-hover); }
</style>