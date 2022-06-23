<template>
  <html>
    <header>
      <h1>
        <div id="app-title">
          Grade Manager
        </div>
      </h1>
    </header>

    <main>
      <router-view />
      <!---<TheWelcome />-->
    </main>
  </html>
</template>

<style>
@import './assets/style.css';
</style>

<style lang="scss">
#app {
  font-family: Calibri, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000000;
}

h1 {
  background-color: transparent;
}
</style>
