<template>
  <div class="calendar-widget">
    <div class="calendar-header">
      <div class="month-title-wrapper">
        <span class="month-title">{{ monthNames[currentMonth] }} {{ currentYear }}</span>
        <!-- Добавлена декоративная стрелка возле месяца -->
        <span class="month-arrow-icon">&gt;</span>
      </div>
      
      <div class="cal-arrows">
        <span class="arrow" @click="changeMonth(-1)">&lt;</span>
        <span class="arrow" @click="changeMonth(1)">&gt;</span>
      </div>
    </div>
    
    <div class="calendar-grid">
      <!-- Заголовки дней недели -->
      <div class="day-name" v-for="d in daysOfWeek" :key="d">{{ d }}</div>

      <!-- Генерация чисел -->
      <div 
        v-for="(day, index) in calendarDays" 
        :key="index"
        class="day-number" 
        :class="{
          'prev-month': !day.isCurrentMonth,
          'next-month': !day.isCurrentMonth,
          'active': day.isActive,
          'is-weekend': day.isWeekend
        }"
        @click="selectDate(day)"
      >
        {{ day.date }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const daysOfWeek = ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс']
const monthNames = ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь']

// Реактивные переменные для управления календарем
const currentYear = ref(2023)
const currentMonth = ref(11) // 0 - Январь, 11 - Декабрь. Начинаем с декабря 2023
const selectedDay = ref(13) // Изначально выделено 13 число

// Функция переключения месяца
const changeMonth = (delta) => {
  currentMonth.value += delta
  if (currentMonth.value > 11) {
    currentMonth.value = 0
    currentYear.value += 1
  } else if (currentMonth.value < 0) {
    currentMonth.value = 11
    currentYear.value -= 1
  }
  // При смене месяца сбрасываем выбор на 1-е число, чтобы не было пустоты
  selectedDay.value = 1
}

// Функция выбора даты
const selectDate = (day) => {
  if (day.isCurrentMonth) {
    selectedDay.value = day.date
  }
}

// Вычисляемое свойство для генерации сетки календаря
const calendarDays = computed(() => {
  const year = currentYear.value
  const month = currentMonth.value

  const firstDayOfMonth = new Date(year, month, 1)
  let offset = firstDayOfMonth.getDay() - 1
  if (offset < 0) offset = 6

  const startDate = new Date(year, month, 1 - offset)
  const days = []

  // Генерируем 42 ячейки (6 недель)
  for (let i = 0; i < 42; i++) {
    const currentDate = new Date(startDate)
    currentDate.setDate(startDate.getDate() + i)
    
    const dayOfWeek = currentDate.getDay() // 0=Вс, 6=Сб
    
    days.push({
      date: currentDate.getDate(),
      isCurrentMonth: currentDate.getMonth() === month,
      isWeekend: dayOfWeek === 6 || dayOfWeek === 0,
      isActive: currentDate.getMonth() === month && currentDate.getDate() === selectedDay.value
    })
  }
  return days
})
</script>

<style scoped>
.calendar-widget {
  width: 100%;
  background: #F2F2F2; /* Серый фон */
  border-radius: 6px;
  padding: 16px;
  box-sizing: border-box;
}

/* Обновленный заголовок календаря */
.calendar-header {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 16px;
  margin-bottom: 16px;
}

/* Группируем месяц и стрелку рядом */
.month-title-wrapper {
  display: flex;
  align-items: center;
  gap: 6px;
}

.month-title {
  font-family: 'Nunito Sans', sans-serif;
  font-weight: 700;
  font-size: 20px;
  line-height: 24px;
  letter-spacing: 0.38px;
  color: #000;
}

/* Декоративная стрелка возле месяца */
.month-arrow-icon {
  color: #686868;
  font-size: 14px;
  font-weight: bold;
  cursor: default; /* Она не кликабельная */
}

/* Основные стрелки переключения */
.cal-arrows {
  display: flex;
  gap: 10px;
}

.arrow {
  color: #686868;
  cursor: pointer;
  font-size: 14px;
  font-weight: bold;
  transition: opacity 0.2s;
}
.arrow:hover { opacity: 0.7; }

.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  text-align: center;
  color: #333;
  row-gap: 6px;
}

.day-name { 
  font-weight: 600; 
  color: #004636; /* Цвет дней недели */
  font-size: 12px; 
  margin-bottom: 6px; 
  padding-bottom: 4px;
}

.day-number { 
  padding: 6px 0; 
  cursor: pointer; 
  position: relative;
  border-radius: 6px;
  transition: all 0.2s;
  color: #333;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 32px;
  margin: 0 auto;
  aspect-ratio: 1 / 1; /* Идеально квадратная форма */
}

.day-number:hover { background: #dbeae5; }

/* Стили для дней из прошлого/будущего месяца (полупрозрачные) */
.prev-month, .next-month {
  opacity: 0.5;
  color: #888;
}

/* ВЫХОДНЫЕ ДНИ текущего месяца: перекрашиваем цифры в красный */
.is-weekend {
  color: #D12E2E !important;
}

/* ВЫХОДНЫЕ ДНИ из других месяцев: красные, но полупрозрачные */
.prev-month.is-weekend, .next-month.is-weekend {
  color: #D12E2E;
  opacity: 0.5;
}

/* Выбранный день (зеленый квадрат с круглыми уголками) */
.day-number.active { 
  background: #497c6b; 
  color: white !important; 
  font-weight: 600;
  border-radius: 6px;
}
.day-number.active:hover { background: #3d6658; }
</style>