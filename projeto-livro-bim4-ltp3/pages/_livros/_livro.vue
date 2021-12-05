<template>
  <div>
    <NavBar />
    <div class="mt-5 d-flex justify-content-center">
      <b-card
        header="ATENÇÃO!"
        header-tag="header"
        header-text-variant="h1 font-weight-bold"
        header-bg-variant="danger text-light text-center"
        class="border-danger"
      >
        <b-card-text class="text-center text-danger">
          O livro foi excluido com sucesso!
        </b-card-text>
        <div class="justify-content-center mb-3 border-bottom pb-3 border-danger d-flex"><b-img src="https://i.imgur.com/VvSggmt.png" width="100px"></b-img></div>
        <b-button variant="outline-primary"
          ><NuxtLink class="links" to="../"
            >Voltar para o início</NuxtLink
          ></b-button
        >
        <b-button variant="outline-success"
          ><NuxtLink class="links" to="../criar-livro"
            >Voltar para criação de livros</NuxtLink
          ></b-button
        >
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    let livro
    try {
      livro = await $axios.$delete(`/livros/deletar/${params.livro}`)
    } catch (e) {
      console.log(e)
    }
    console.log(JSON.stringify(livro))
    return { livro }
  },
}
</script>
  
<style>
body{ font-size:22px;}
.links,
.links:link,
.links:hover {
  color: inherit;
  text-decoration: inherit;
}
</style>