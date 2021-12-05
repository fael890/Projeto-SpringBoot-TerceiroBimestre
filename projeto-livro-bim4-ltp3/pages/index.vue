<template>
  <div>
    <NavBar />
    <div>
      <b-table thead-class="bg-dark text-light" class="table" :items="livros" :fields="fields" hover responsive="sm">
        <template #cell(apagar)="data">
          <NuxtLink :to="`/livros/${data.item.id}`">
            <b-button variant="outline-danger">Excluir</b-button>
          </NuxtLink>
        </template>
        <template id="template-show" #cell(show_details)="row">
          <b-button variant="outline-primary"  @click="row.toggleDetails" class="mr-2">
            {{ row.detailsShowing ? 'Esconder' : 'Mostrar' }} Detalhes
          </b-button>

          <!-- <b-form-checkbox
            v-model="row.detailsShowing"
            @change="row.toggleDetails"
          >
            Mostrando detalhes
          </b-form-checkbox> -->
        </template>

        <template #row-details="row">
          <b-card>
            <b-row class="mb-2">
              <b-col sm="3" class="text-sm-right"><b>Nº de Páginas:</b></b-col>
              <b-col>{{ row.item.rotulo.numPages }}</b-col>
            </b-row>

            <b-row class="mb-2">
              <b-col sm="3" class="text-sm-right"><b>Sinopse:</b></b-col>
              <b-col>{{ row.item.rotulo.sinopse }}</b-col>
            </b-row>

            <b-row class="mb-2">
              <b-col sm="3" class="text-sm-right"><b>Categoria:</b></b-col>
              <b-col>{{ row.item.categorias[0].categoria }}</b-col>
            </b-row>

            <b-row class="mb-2">
              <b-col sm="3" class="text-sm-right"><b>Descricao:</b></b-col>
              <b-col>{{ row.item.categorias[0].descricao }}</b-col>
            </b-row>

            <!-- <b-button size="sm" @click="row.toggleDetails"
              >Esconder Detalhes</b-button
            > -->
          </b-card>
        </template>
      </b-table>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    let livros
    try {
      livros = await $axios.$get('/livros/listagem-livros')
    } catch (e) {
      console.log(e)
    }
    console.log(JSON.stringify(livros))
    return { livros }
  },

  data: () => {
    return {
      fields: [
        {
          key: 'title',
          label: 'Titulo',
        },
        {
          key: 'lido',
          label: 'Lido',
        },
        {
          key: 'show_details',
          label: 'Detalhes',
        },
        {
          key: 'apagar',
          label: 'Excluir livro'
        },
      ],
    }
  },
}
</script>
  
<style>
  body{
    font-size: 20px;
  }
  .table td{
    border-bottom:1px solid black ;
  }
</style>
