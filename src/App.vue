<script setup>
import { ref, reactive, computed } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'

const rawHtml = reactive('<span style="color: red">이것은 빨간색이어야 합니다.</span>');
const dynamicId = reactive('aa');

const state = { isButtonDisabled: ref(true) };

function toggleButtonDisabled() {
  state.isButtonDisabled.value = !state.isButtonDisabled.value;
}

const buttonText = computed(() => {
  return state.isButtonDisabled.value ? '버튼Off' : '버튼On';
})

const isActive = ref(true)
const hasError = ref(false)

const classObject = reactive({
  active: true,
  'text-danger': false
})


</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <!-- <TheWelcome /> -->
    <button @click="toggleButtonDisabled">Disabled Toggle</button>
    <button class="static" :class="classObject" :disabled="state.isButtonDisabled.value">{{buttonText}}</button>
    <div v-bind:id="dynamicId">1</div>
    <p>텍스트 보간법 사용: {{ rawHtml }}</p>
    <p>v-html 디렉티브 사용: <span v-html="rawHtml"></span></p>

  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

.active {
  font-weight: bold;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
