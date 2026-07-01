<template>
  <div class="calendar-widget">
    <div class="calendar-header">
      <span class="month-title">Декабрь 2023</span>
      <div class="cal-arrows">
        <span class="arrow">&lt;</span>
        <span class="arrow">&gt;</span>
      </div>
    </div>
    <div class="calendar-grid">
      <!-- Заголовки дней недели -->
      <div class="day-name" v-for="d in daysOfWeek" :key="d">{{ d }}</div>

      <!-- Генерация чисел (6 строк по 7 дней = 42 ячейки) -->
      <div 
        class="day-number" 
        v-for="(day, index) in days" 
        :key="index"
        :class="{
          'prev-month': !day.isCurrentMonth && day.date > 20,
          'next-month': !day.isCurrentMonth && day.date < 10,
          'current-month': day.isCurrentMonth,
          'active': day.isActive,
          'is-weekend': day.isWeekend
        }"
      >
        {{ day.date }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const daysOfWeek = ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс']

// Генерация календаря для Декабря 2023 (6 недель, 42 дня)
const generateCalendar = () => {
  const year = 2023
  const month = 11 // Декабрь (в JS месяцы: 0 - Январь, 11 - Декабрь)
  
  const firstDayOfMonth = new Date(year, month, 1)
  let offset = firstDayOfMonth.getDay() - 1 
  if (offset < 0) offset = 6 

  const startDate = new Date(year, month, 1 - offset)
  
  const days = []
  for (let i = 0; i < 42; i++) {
    const currentDate = new Date(startDate)
    currentDate.setDate(startDate.getDate() + i)
    
    const dayOfWeek = currentDate.getDay() // 0=Вс, 6=Сб
    
    days.push({
      date: currentDate.getDate(),
      isCurrentMonth: currentDate.getMonth() === month,
      isWeekend: dayOfWeek === 6 || dayOfWeek === 0,
      isActive: currentDate.getDate() === 13 && currentDate.getMonth() === month 
    })
  }
  return days
}

const days = ref(generateCalendar())
</script>

<style scoped>
.calendar-widget {
  width: 100%;
  background: #F2F2F2; /* Добавлен серый фон */
  border-radius: 6px;   /* Скругление самого блока календаря */
  padding: 16px;
  box-sizing: border-box;
}

.calendar-header {
  display: flex;
  justify-content: flex-start; /* Координаты не меняются, заголовок слева */
  align-items: center;
  gap: 16px;
  margin-bottom: 16px;
}

.month-title {
  font-family: 'Nunito Sans', sans-serif;
  font-weight: 700;
  font-size: 20px;
  line-height: 24px;
  letter-spacing: 0.38px;
  color: #000;
}

.cal-arrows {
  display: flex;
  gap: 10px;
}

.arrow {
  color: #686868; /* Указанный цвет стрелок */
  cursor: pointer;
  font-size: 14px;
  font-weight: bold;
}

.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  text-align: center;
  color: #333;
  row-gap: 6px;
}

.day-name { 
  font-weight: 600; 
  color: #004636; /* Изменен цвет дней недели */
  font-size: 12px; 
  margin-bottom: 6px; 
  padding-bottom: 4px;
}

.day-number { 
  padding: 6px 0; 
  cursor: pointer; 
  position: relative;
  border-radius: 6px; /* Изначально скругление для обычных дней */
  transition: all 0.2s;
  color: #333;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 32px; /* Фиксированная высота для идеального квадрата */
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
  border-radius: 6px; /* Квадратная форма с круглыми уголками */
}
.day-number.active:hover { background: #3d6658; }
</style>