<template>
  <div class="home">
    <p>
      Go to page <router-link to="/todos">Todos</router-link>
    </p>
  </div>
</template>

<style scoped lang="scss">
@import "../styles/variables";

p {
  text-align: center;
  font-size: 24px;
  color: #000;
}

a {
  text-decoration: none;
  color: $color-red;
}
</style>
