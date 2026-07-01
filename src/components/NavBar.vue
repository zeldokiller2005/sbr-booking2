<template>
  <nav class="navbar">
    <div class="nav-inner">
      <div class="nav-left">
        <img :src="logoIcon" class="nav-logo" alt="Logo" />
      </div>

      <div class="nav-links">
        <!-- Динамические классы для переключения подчеркивания (border-bottom: 1px solid #FFFFFF) -->
        <div class="nav-link" :class="{ active: currentView === 'apparatus' }">Аппаратура</div>
        <div class="nav-link" :class="{ active: currentView === 'people' }" @click="$emit('update-view', 'people')">Люди</div>
        <div class="nav-link" :class="{ active: currentView === 'space' }" @click="$emit('update-view', 'space')">Пространство</div>
        
        <div class="nav-link profile-wrapper" @click="toggleProfile">
          <span class="profile-text">Профиль</span>
          <img :src="avatarIcon" class="avatar-icon" alt="Профиль" />
          <ProfilePopup v-if="isProfileOpen" @close="isProfileOpen = false" />
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue'
import ProfilePopup from './ProfilePopup.vue'
import logoIcon from '../assets/logo.png'    
import avatarIcon from '../assets/avatar.png' 

// Добавили принятие пропса currentView
const props = defineProps({
  currentView: String
})

defineEmits(['update-view'])
const isProfileOpen = ref(false)
const toggleProfile = () => { isProfileOpen.value = !isProfileOpen.value }
</script>

<style scoped>
.navbar {
  position: absolute;
  top: 950px;
  left: 0;
  width: 100%;
  height: 84px;
  background-color: rgba(21, 21, 20, 0.8); /* #151514 с прозрачностью 80% */
  padding: 10px 50px;
  box-sizing: border-box;
  border-top: none;
  display: flex;
  align-items: center;
  z-index: 10;
}

.nav-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: 1920px;
  margin: 0 auto;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 40px;
}

.nav-logo {
  width: 32px;
  height: 32px;
  object-fit: contain;
}

.nav-link {
  color: #ddd;
  cursor: pointer;
  font-weight: 500;
  font-size: 16px;
  transition: color 0.2s;
  position: relative;
}

.nav-link:hover { color: #ffffff; }

/* Динамически добавляемое подчеркивание по 1px #FFFFFF */
.nav-link.active {
  color: #ffffff;
  border-bottom: 1px solid #FFFFFF;
  padding-bottom: 4px;
}

/* Блок профиля */
.profile-wrapper {
  display: flex;
  align-items: center;
  gap: 12px;
  position: relative;
}

.profile-text { color: #ddd; }

.avatar-icon {
  width: 36px;
  height: 36px;
  object-fit: contain;
  border-radius: 50%;
}
</style>