<script>
export default {
  data() {
    return {
      activeIndex: 0, // то, что позволяет определить текущий активный шаг
      steps: [
        {
          title: 'Основы',
          text: 'В блоке вы познакомитесь со всеми основами Vue.js на практике. На протяжении блока мы напишем реактивное приложение, в процессе разработки которого разберем вся базу фреймворка.'
        },
        {
          title: 'Компоненты',
          text: 'Один из самых важных блоков в курсе, где вы узнаете все о компонентах. В блоке мы напишем 2 разных приложения и создадим более 5 различных UI компонентов как в реальной разработке. Блок расскажет про абсолютно все составляющие, которые есть в компонентах: взаимодействие, slots, асинхронные и динамические компоненты и тонна примеров.'
        },
        {
          title: 'Роутер',
          text: 'В данном блоке вы узнаете все о том, как работает мультиязычность во Vue. Мы создадим миниклон Gmail в данном блоке, где вы на практике увидите как работать с динамическим роутером.'
        },
        {
          title: 'Vuex',
          text: 'В блоке вы узнаете абсолютно все про Vuex. Вы узнаете как работать с данными, какие есть лучшие практики по их программированию и структурированию. Все на практике.'
        },
        {
          title: 'Composition',
          text: 'Одним из наиболее важных обновлений в Vue 3 является появление альтернативного синтаксиса Composition API. В этом блоке вы узнаете все, чтобы полностью пользоваться данными синтаксисом на практических примерах. Помимо этого вы узнаете как работать совместно с Vue Router и Vuex.'
        }
      ],
      isLasted: true
    }
  },
  methods: {
    prev() {
      // когда нажимаем кнопку назад
      if (this.activeIndex !== 0) {
        this.activeIndex--
      }
    },
    reset() {
      // начать заново
      this.activeIndex = 0
      this.isLasted = true
    },
    nextOfFinish() {
      // кнопка вперед или закончить
      if (this.activeIndex !== this.steps.length - 1) {
        this.activeIndex++
      } else {
        this.isLasted = false
      }
    },
    setActive(idx) {
      // когда нажимаем на определенный шаг
      this.activeIndex = idx
    }
  },
  computed: {
    // тут стоит определить несколько свойств:
    // 1. текущий выбранный шаг
    // 2. выключена ли кнопка назад
    // 3. находимся ли мы на последнем шаге
    activeStep() {
      return this.steps[this.activeIndex]
    },
    prevDisabled() {
      return this.activeIndex === 0
    },
    lastStep() {
      return this.activeIndex === this.steps.length - 1
    }
  }
}
</script>

<template>
  <div class="card">
    <h1>План по изучению Vue.js</h1>

    <div class="steps">
      <div class="steps-content">
        {{ activeStep.text }}
      </div>
      <ul class="steps-list">
        <li
          class="steps-item"
          :class="{ active: activeIndex === ind, done: ind < activeIndex }"
          v-for="(step, ind) in steps"
          :key="ind"
          @click="setActive(ind)"
        >
          <span>{{ ind + 1 }}</span
          >{{ step.title }}
        </li>
      </ul>
      <div v-if="isLasted">
        <button class="btn" :disabled="prevDisabled" @click="prev">Назад</button>
        <button class="btn primary" @click="nextOfFinish">
          {{ !lastStep ? 'Вперед' : 'Закончить' }}
        </button>
      </div>
      <div v-else>
        <button class="btn" @click="reset">Начать заново</button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
