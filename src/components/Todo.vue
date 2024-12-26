<template>
  <!-- Основной блок -->
  <div v-if="!isEdit">
    <div title="Что бы пометить как выполнено нажми сюда, если хочешь вернутся к заданию нажми еще раз " class="unit"
      :class="{ start: !isActive, done: isActive }"
       @click="toggleClass()">
      {{ point }}
    </div>
    <br>
    <button @click="edit">Редактировать</button>
  </div>

  <!-- Блок редактирования -->
  <div v-else>
    <input v-model="newPoint">
    <button @click="save">Сохранить</button>
  </div>

  <div>
     <button @click="remove">Удалить</button>
  </div><!-- Кнопка удаления -->
 
  <hr>
  <br>
</template>

<script>
export default {
  // Регистрация событий для передачи данных родительскому компоненту
  emits: ['remove', 'change'],
  props: {
    id: Number,
    point: String,
  },
  data() {
    return {
      newPoint: '',
      isEdit: false,
      isActive: false
    };
  },
  methods: {
    remove() {
      this.$emit('remove', this.id);
    },
    edit() {
      this.newPoint = this.point; // Сохраняем текущее значение перед редактированием
      this.isEdit = true;
    },
    save() {
      this.isEdit = false;
      this.$emit('change', this.id, this.newPoint); // Передаем новое значение через событие
    },
    toggleClass() {
      this.isActive = !this.isActive
    }
  },
};
</script>

<style>
/* Основные стили */
.unit {
  display: inline-block;
  padding: 10px;
  margin-bottom: 8px;
  border-radius: 5px;
  background-color: #f9f9f9;
  transition: all 0.3s ease-in-out;
}

/* Стиль для невыполненного задания */
.start {
  color: #333;
  cursor: pointer;
  user-select: none;
}

/* Стиль для выполненного задания */
.done {
  color: #888;
  cursor: pointer;
  user-select: none;
  text-decoration: line-through;
}


</style>