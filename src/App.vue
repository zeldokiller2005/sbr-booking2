<template>
  <div class="app-wrapper">
    <div class="hero-wrapper">
      <Header />
      <!-- Добавили :current-view="activeView" -->
      <NavBar @update-view="activeView = $event" :current-view="activeView" />
    </div>

    <div class="main-area container">
      <div v-if="activeView === 'people'" class="view-people">
        <div class="toolbar">
          <div class="search-block">
            <input type="text" placeholder="Поиск" class="search-input" />
            <span class="icon-filter">⚲</span>
            <div class="filter-group">
              <span>По алфавиту</span>
              <span class="dropdown-icon">∨</span>
            </div>
          </div>
          <button class="btn-primary btn-add" @click="toggleModal('newEvent')">Добавить +</button>
        </div>

        <div class="grid-users">
          <UserCard 
            v-for="(user, index) in users" 
            :key="index" 
            :name="user.name" 
            :bio="user.bio" 
            :avatar="user.avatar"
            :badge="user.badge"
            @invite="console.log('Invite clicked')"
            @details="console.log('Details clicked')"
          />
        </div>
      </div>

      <div v-else-if="activeView === 'space'" class="view-space">
        <div class="space-list">
          <SpaceCard 
            v-for="(space, index) in spaces" 
            :key="index"
            :title="space.title" 
            :image="space.image"
            @book="toggleModal('booking')"
            @more="console.log('More clicked')"
          />
        </div>
      </div>

      <aside class="right-sidebar">
        <CalendarWidget />
        <div class="sidebar-divider"></div>
        <div class="active-invites-section">
          <h3>Активные приглашения</h3>
          <InvitationList 
            v-for="(invite, index) in invites" 
            :key="index" 
            :title="invite.title" 
            :time="invite.time" 
            :person="invite.person"
            :role="invite.role" 
          />
        </div>
      </aside>
    </div>

    <ModalNewEvent v-if="modalType === 'newEvent'" @close="closeModal" @submit="handleBooking" />
    <ModalBooking v-else-if="modalType === 'booking'" @close="closeModal" @submit="handleBooking" />
    <ModalError v-else-if="modalType === 'error'" @close="closeModal" />
  </div>
</template>

<script setup>
import { ref } from 'vue'

import Header from './components/Header.vue'
import NavBar from './components/NavBar.vue'
import UserCard from './components/UserCard.vue'
import SpaceCard from './components/SpaceCard.vue'
import CalendarWidget from './components/CalendarWidget.vue'
import InvitationList from './components/InvitationList.vue'
import ModalNewEvent from './components/ModalNewEvent.vue'
import ModalBooking from './components/ModalBooking.vue'
import ModalError from './components/ModalError.vue'

import ivanImg from './assets/ivan.jpg'
import anastasiaImg from './assets/anastasia.jpg'
import coworkingImg from './assets/coworking.jpg'
import officeImg from './assets/office.jpg'

const activeView = ref('people') // По умолчанию "Люди"
const modalType = ref(null)

const users = [
  { name: 'Иван Иванов', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: ivanImg, badge: 'Фотограф' },
  { name: 'Анастасия Ремогузина', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: anastasiaImg, badge: 'Фотограф' },
  { name: 'Иван Иванов', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: ivanImg, badge: 'Фотограф' },
  { name: 'Анастасия Ремогузина', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: anastasiaImg, badge: 'Фотограф' },
  { name: 'Иван Иванов', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: ivanImg, badge: 'Фотограф' },
  { name: 'Анастасия Ремогузина', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: anastasiaImg, badge: 'Фотограф' },
  { name: 'Иван Иванов', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: ivanImg, badge: 'Фотограф' },
  { name: 'Анастасия Ремогузина', bio: 'Высококачественная видеосъёмка и аэросъёмка: доступные цены, профессиональное оборудование и опытные специалисты', avatar: anastasiaImg, badge: 'Фотограф' }
]

const spaces = [
  { title: 'Коворкинг ИРНИТУ', image: coworkingImg },
  { title: 'Переговорная ИРНИТУ', image: officeImg }
]

const invites = [
  { title: 'Съёмки в первомайском', time: '10:00 - 12:00', person: 'Иванов И. В.', role: 'Фотограф' },
  { title: 'Съёмки в первомайском', time: '10:00 - 12:00', person: 'Иванов И. В.', role: 'Фотограф' }
]

const toggleModal = (type) => { modalType.value = type }
const closeModal = () => { modalType.value = null }
const handleBooking = () => { modalType.value = 'error' }
</script>

<style scoped>
.app-wrapper { display: flex; flex-direction: column; min-height: 100vh; align-items: center; overflow-x: hidden; /* Защита от горизонтального скролла */ }

.hero-wrapper {
  position: relative;
  width: 100%;
  max-width: 1920px;
}

.main-area {
  display: flex;
  gap: 24px; /* Увеличили отступ между контентом и боковой панелью */
  padding-top: 30px;
  align-items: flex-start;
  width: 100%;
  max-width: 1440px;
  margin: 0 auto;
  box-sizing: border-box; /* Важно: считает padding в ширину */
}

.view-people { flex: 1; width: 100%; min-width: 0; /* Защита от переполнения flex-элемента */ }
.view-space { flex: 1; min-width: 0; }

.toolbar {
  display: flex;
  justify-content: space-between;
  margin-bottom: 24px;
}

.search-block {
  display: flex;
  align-items: center;
  background: white;
  padding: 10px 16px;
  border-radius: 6px;
  gap: 12px;
  border: 1px solid transparent;
}
.search-block:hover { border-color: #d1d1d1; }
.search-input { border: none; background: transparent; width: 250px; font-size: 14px; }
.icon-filter { color: #888; margin-right: 8px; }
.filter-group {
  display: flex;
  align-items: center;
  background: #f5f5f5;
  padding: 6px 10px;
  border-radius: 4px;
  font-size: 13px;
  color: #555;
  cursor: pointer;
  gap: 6px;
}
.btn-add { border-radius: 6px; padding: 10px 24px; font-weight: 500; }

.grid-users {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
  width: 100%;
}

/* РАСШИРЯЕМ КОЛОНКУ ДО 360px */
.right-sidebar {
  width: 360px; 
  flex-shrink: 0;
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-sizing: border-box;
  min-height: 400px;
}

.sidebar-divider { height: 1px; background: #eaeaea; margin: 12px 0; }
.active-invites-section h3 { font-size: 16px; font-weight: 500; margin-bottom: 16px; }

.space-list { display: flex; flex-direction: column; gap: 24px; }
</style>