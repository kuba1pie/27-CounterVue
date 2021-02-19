<template>
  <div id="app">
    <header>
      <b-button variant="primary"
        ><router-link to="/">App</router-link></b-button
      >
      <b-button variant="primary"
        ><router-link to="/about">About Me</router-link></b-button
      >
    </header>
    <main><router-view /></main>
    <footer class="footer">
      <a href="https:kubapietruszewski.pl/vuecounter">KubaPietruszewski.pl</a>
    </footer>
  </div>
</template>
