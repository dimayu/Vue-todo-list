<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/todos">Todos</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
@import 'styles/reset';
@import "styles/variables";

body {
  font-family: 'Roboto', sans-serif;
  background-color: $bg;
  font-style: normal;
  font-weight: 300;
  font-size: 16px;
  line-height: 1.2;
  color: $color-red;
  overflow: hidden;
}

#app {
  height: 100%;
  display: flex;
  flex-direction: column;
}

nav {
  padding: 12px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: $color-red;
    }
  }
}

.todo {
  width: 50%;
  max-width: 940px;
  min-width: 300px;
  position: relative;
  margin: 2% auto;
  background-color: #fff;
  border-radius: 20px;
  box-sizing: border-box;
  overflow: hidden;
}

.wrapper {
  width: 100%;
  box-sizing: border-box;
  padding: 12px;
}
</style>
