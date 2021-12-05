<template>
  <div>
    <b-navbar toggleable type="dark" variant="primary">
      <b-navbar-brand href="/">
        <img
          src="../static/image/livro-logo-white.png"
          class="logo d-inline-block align-top"
        />
      </b-navbar-brand>

      <b-navbar-toggle target="navbar-toggle-collapse">
        <template #default="{ expanded }">
          <b-icon v-if="expanded" font-scale="1.5" class="text-center text-light" icon="chevron-bar-up"></b-icon>
          <b-icon v-else font-scale="1.5" class="text-center text-light" icon="chevron-bar-down"></b-icon>
        </template>
      </b-navbar-toggle>

      <b-collapse id="navbar-toggle-collapse" is-nav>
        <b-navbar-nav class="links ml-auto">
          <b-nav-item><NuxtLink class="link" :to="`/`">HOME</NuxtLink></b-nav-item>
          <b-nav-item><NuxtLink class="link" :to="`/criar-livro`">CRIAR LIVRO</NuxtLink></b-nav-item>
          <b-nav-item><NuxtLink class="link" :to="`/listagem-livro-id`">LISTAR LIVROS</NuxtLink></b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<style scoped>
.logo {
  width: 60px;
}
.navbar {
  font-size: 24px;
}
.link{
  color: aliceblue;
}
.navbar-toggler{
  border:1.5px solid white;
}
</style>