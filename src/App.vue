<template>
  <section class="section">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <img src="/images/logo.svg" height="60" />

        <a
          role="button"
          class="navbar-burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbarBasicExample"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>
      <div id="navbarMain" class="navbar-menu">
        <div class="navbar-end">
          <router-link to="/" class="navbar-item"> Dashoard </router-link>
          <router-link to="/recipes/all" class="navbar-item">
            All Recipes
          </router-link>
          <router-link to="/recipes/create" class="navbar-item">
            Create Recipe
          </router-link>
          <div class="field mt-1">
            <div class="control has-icons-left">
              <input
                type="text"
                name="search"
                placeholder="Search"
                class="input is-rounded"
              />
              <span class="icon is-small is-left">
                <i class="fas fa-search"></i>
              </span>
            </div>
          </div>
        </div>
      </div>
    </nav>
  </section>
  <router-view />
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
