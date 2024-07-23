<script setup>
import { ref } from 'vue';
import Button from "./components/Button.vue";

const display = ref("");
const MAX_LENGTH = 10; // Максимальное количество символов на дисплее

// Определение отформатированного текста для дисплея
function formattedDisplay() {
  if (display.value.length > MAX_LENGTH) {
    return display.value.slice(0, MAX_LENGTH) + '...';
  }
  return display.value || "0"; // Показываем 0, если дисплей пуст
}

// Удаление последнего символа
function deleteLast() {
  display.value = display.value.slice(0, -1);
}

// Очистка дисплея
function clearDisplay() {
  display.value = "";
}

// Добавление цифры или знака
function addSymbol(symbol) {
  display.value += symbol;
}

// Вычисление результата
function calculate() {
  try {
    display.value = eval(display.value).toString();
  } catch (e) {
    display.value = "Ошибка";
  }
}
</script>

<template>
  <h1>Думайте.</h1>

  <div class="calculator">
    <div class="display" :class="{ 'empty': display.value === '' }">
      <h2>{{ formattedDisplay() }}</h2>
    </div>
    <div class="container">
      <Button sym="C" :foo="deleteLast" />
      <Button sym="CE" :foo="clearDisplay" />
      <Button sym="*" :foo="() => addSymbol('*')" />
      <Button sym="/" :foo="() => addSymbol('/')" />
      <Button sym="+" :foo="() => addSymbol('+')" />
      <Button sym="-" :foo="() => addSymbol('-')" />
      <Button sym="7" :foo="() => addSymbol('7')" />
      <Button sym="8" :foo="() => addSymbol('8')" />
      <Button sym="9" :foo="() => addSymbol('9')" />
      <Button sym="4" :foo="() => addSymbol('4')" />
      <Button sym="5" :foo="() => addSymbol('5')" />
      <Button sym="6" :foo="() => addSymbol('6')" />
      <Button sym="1" :foo="() => addSymbol('1')" />
      <Button sym="2" :foo="() => addSymbol('2')" />
      <Button sym="3" :foo="() => addSymbol('3')" />
      <Button sym="0" :foo="() => addSymbol('0')" />
      <Button sym="." :foo="() => addSymbol('.')" />
      <Button sym="=" :foo="calculate" />
    </div>
  </div>
</template>
<style scoped>
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3px;
}
.calculator {
  border-width: 3px;
  border-style: solid;
  border-color: black;
  border-radius: 10px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
h2 {
  text-align: right; /* Меняем выравнивание на правое для калькулятора */
  margin: 10px;
}
.display {
  height: 50px; /* Задаем фиксированную высоту для дисплея */
  display: flex;
  align-items: center; /* Вертикальное выравнивание текста */
}

.empty {
  height: 50px; /* Фиксированная высота при пустом дисплее */
}

/* Медиа-запрос для мобильных устройств */
@media (max-width: 1000px) { /* Ограничение для мобильных устройств */
  .calculator {
    transform: scale(1.5); /* Увеличиваем размер калькулятора в 2 раза */
    transform-origin: top center; /* Устанавливаем точку начала трансформации */
  }

  .display h2 {
    font-size: 2em; /* Увеличиваем размер шрифта в 2 раза */
  }

  .container {
    gap: 6px; /* Увеличиваем отступы между кнопками */
  }
}
h1{
  height: 2lh;
}
</style>