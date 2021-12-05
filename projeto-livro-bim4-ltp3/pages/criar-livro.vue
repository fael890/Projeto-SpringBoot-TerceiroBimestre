<template>
  <div>
    <NavBar />
    <div class="mt-5 py-4 container">
      <div class="mb-4 title">
        <h1 >Criar novo livro</h1>
      </div>
      <b-form @submit="criarLivro">
        <b-form-group
          id="input-group-1"
          label="Título do livro:"
          label-for="title"
        >
          <b-form-input
            id="title"
            v-model="form.title"
            placeholder="Digite o título..."
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Lido:">
          <b-form-checkbox
            id="lido"
            v-model="form.lido"
            value="true"
            class="lido"
            required
          >Lido</b-form-checkbox>
        </b-form-group>

        <b-form-group id="input-group-3">
          <b-form-checkbox
            id="lido"
            value="false"
            class="lido"
            required
          >Não lido</b-form-checkbox>
        </b-form-group>

        <b-form-group id="input-group-4" label="Sinopse:" label-for="rotulo">
          <b-form-textarea
            id="rotulo"
            v-model="form.rotulo.sinopse"
            placeholder="Digite a sinopse..."
            required
          ></b-form-textarea>
        </b-form-group>

        <b-form-group
          id="input-group-5"
          label="Número de páginas:"
          label-for="numPages"
        >
          <b-form-input
            type="number"
            id="numPages"
            v-model="form.rotulo.numPages"
            placeholder="Digite o número de páginas..."
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-6"
          label="Categorias:"
          label-for="categoria"
        >
          <b-form-select
            id="categoria"
            v-model="form.categorias[0].categoria"
            :options="categorias"
            :value="null"
            placeholder="Escolha a categoria..."
            required
          ></b-form-select>
        </b-form-group>

        <b-form-group
          id="input-group-7"
          label="Descrição categoria:"
          label-for="categoria"
        >
          <b-form-input
            id="categoria"
            v-model="form.categorias[0].descricao"
            placeholder="Descrição da categoria"
            required
          ></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="outline-primary">Criar</b-button>
        <b-button type="reset" variant="outline-danger">Limpar</b-button>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      form: {
        title: '',
        lido: '',
        rotulo: {
          sinopse: '',
          numPages: '',
        },
        categorias: [
          {
            categoria: '',
            descricao: '',
          },
        ],
      },
      categorias: [
        { text: 'Selecione uma categoria', value: null },
        'Tensão',
        'Ação',
        'Aventura',
        'Ficção Científica',
        'Romace',
        'Terror',
      ],
    }
  },
  methods: {
    async criarLivro(event) {
      event.preventDefault()
      try {
        const dataLivro = await this.$axios.$post('/livros/criar', this.form)
        console.log(this.form)
        if (dataLivro !== null) {
          this.$bvModal.msgBoxOk('O novo livro foi criado com sucesso!', {
            title: 'Confirmation',
            size: 'sm',
            buttonSize: 'sm',
            okVariant: 'success',
            headerClass: 'p-2 border-bottom-0',
            footerClass: 'p-2 border-top-0',
            centered: true,
          })
          this.limparCampos()
        }
      } catch (error) {}
    },
    limparCampos:() =>{
      this.form = {
        title: '',
        lido: '',
        categoria: null,
        rotulo: {
          sinopse: '',
          numPages: '',
        },
        categorias: [
          {
            categoria: '',
            descricao: '',
          },
        ],
      }
    },
  },
}
</script>

<style>
  body{
    font-size: 20px;
  }
  placeholder{
    font-size:20px;
  }
  .lido{
    font-size: 18px;
  }
  .container{
    border: solid 1.2px #007BFF;
    border-radius: 7px;
  }
  .title{
    border-bottom:1.2px solid #007BFF;
  }
</style>