<template>
  <header class="hero" :style="{ backgroundImage: `url(${heroBg})` }">
    
    <div class="center-wrapper">
      <div class="logo-container">
        <img :src="logoIcon" alt="Логотип" class="logo-icon" />
        <div class="logo-text">СБР</div>
        <div class="logo-desc">Сервис бронирования<br>ресурсов</div>
      </div>

      <div class="hero-actions">
        <button class="btn-hero">Вход</button>
        <button class="btn-hero">Регистрация</button>
      </div>

      <div class="hero-subtitle">
        Рыбатекст используется дизайнерами, проектировщиками и фронтендерами, когда нужно быстро заполнить макеты или прототипы содержимым. Это тестовый контент, который не должен нести никакого смысла, лишь показать наличие самого текста или продемонстрировать типографику в деле.
      </div>
    </div>

  </header>
</template>

<script setup>
import heroBg from '../assets/hero-bg.jpg'
import logoIcon from '../assets/logo.png' 
</script>

<style scoped>
.hero {
  width: 100%;
  height: 1035px;
  background-size: cover;
  background-position: center center;
  display: flex;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
}

.center-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 40px;
  width: 100%;
  max-width: 1400px;
  padding: 0 20px;
  box-sizing: border-box;
}

.logo-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 60px;
  color: #FFFFFF;
}

.logo-icon {
  width: 286px;
  height: 286px;
  object-fit: contain;
  flex-shrink: 0;
}

.logo-text {
  font-family: 'Nunito Sans', sans-serif;
  font-weight: 600;
  font-size: 128px;
  line-height: 1;
  letter-spacing: 0px;
  color: #FFFFFF;
}

.logo-desc { 
  font-family: 'Nunito Sans', sans-serif;
  font-weight: 400;
  font-size: 64px;
  line-height: 1;
  letter-spacing: 0px;
  color: #FFFFFF;
  text-align: left;
}

/* Секция с кнопками */
.hero-actions {
  display: flex;
  justify-content: center;
  gap: 24px;
  flex-wrap: wrap;
}

/* Обновленные кнопки с параметрами из Figma */
.btn-hero {
  background: white;
  color: #000000;
  padding: 16px 48px;
  border-radius: 40px;
  font-family: 'Nunito Sans', sans-serif;
  font-weight: 600;      /* SemiBold */
  font-size: 32px;       /* Размер текста */
  line-height: 1;        /* 100% высоты */
  letter-spacing: 0px;   /* 0% межбуквенного интервала */
  cursor: pointer;
  border: none;
}

.hero-subtitle {
  color: rgba(255,255,255,0.95);
  max-width: 650px;
  font-size: 14px;
  line-height: 1.6;
  text-align: center;
}
</style>