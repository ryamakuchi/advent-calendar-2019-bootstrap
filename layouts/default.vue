<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand
        href="https://qiita.com/advent-calendar/2019/nuxt-js"
        target="_blank"
        rel="noopener noreferrer"
      >
        Nuxt.js Advent Calendar 2019 for Qiita
      </b-navbar-brand>

      <b-navbar-nav class="ml-auto">
        <b-nav-item
          href="https://bootstrap-vue.js.org/"
          target="_blank"
          rel="noopener noreferrer"
        >
          Made with BootstrapVue
        </b-nav-item>
      </b-navbar-nav>
    </b-navbar>

    <nuxt />
  </div>
</template>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
</style>
