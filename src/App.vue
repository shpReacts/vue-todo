<template>
  <h1 class="title">todos</h1>
  <Todos />
</template>

<script>
import Todos from '@/components/Todos';

export default {
  name: 'App',
  components: { Todos },
};
</script>

<style lang="scss">
@import '@/assets/colors';

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  font-size: 62.5%;

  @media only screen and (max-width: 720px) {
    font-size: 50%;
  }
}

body {
  box-sizing: border-box;
  font-family: 'Roboto Mono', monospace;
  font-weight: 400;
  line-height: 1.7;
  color: $color-vue-green;
  background-color: $color-vue-blue;
}

#app {
  min-height: 100vh;
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 5rem 0;

  @media only screen and (max-width: 800px) {
    padding: 3rem 0;
  }
}

.title {
  font-size: 10rem;
  font-weight: 100;
  line-height: 1;
  margin-bottom: 3rem;
}
</style>
