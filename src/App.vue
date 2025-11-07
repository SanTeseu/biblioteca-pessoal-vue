@'
<template>
  <div class="app">
    <header><h1>Minha Biblioteca Pessoal</h1></header>
    <p>Total de livros: {{ livros.length }}</p>

    <section class="form-add">
      <h2>Adicionar Novo Livro</h2>
      <form @submit.prevent="adicionarLivro">
        <div>
          <label>Título</label><br/>
          <input v-model="novoLivro.titulo" type="text" />
        </div>
        <div>
          <label>Autor</label><br/>
          <input v-model="novoLivro.autor" type="text" />
        </div>
        <div>
          <label>Ano</label><br/>
          <input v-model.number="novoLivro.ano" type="number" min="1000" max="2024" />
        </div>
        <div>
          <label>Categoria</label><br/>
          <input v-model="novoLivro.categoria" type="text" />
        </div>
        <div>
          <label><input type="checkbox" v-model="novoLivro.lido" /> Lido</label>
        </div>
        <button type="submit">Adicionar</button>
      </form>
    </section>

    <estatisticas-biblioteca :livros="livros" />

    <section class="lista-livros">
      <h2>Meus Livros</h2>
      <div class="grid">
        <cartao-livro
          v-for="livro in livros"
          :key="livro.id"
          :titulo="livro.titulo"
          :autor="livro.autor"
          :ano="livro.ano"
          :lido="livro.lido"
          :categoria="livro.categoria"
          @toggle-lido="alternarLido"
          @remover="removerLivro"
        />
      </div>
    </section>
  </div>
</template>

<script>
import CartaoLivro from './components/CartaoLivro.vue'
import EstatisticasBiblioteca from './components/EstatisticasBiblioteca.vue'

export default {
  name: 'App',
  components: { CartaoLivro, EstatisticasBiblioteca },
  data() {
    return {
      livros: [
        { id: 1, titulo: 'Dom Casmurro', autor: 'Machado de Assis', ano: 1899, lido: true, categoria: 'Literatura' },
        { id: 2, titulo: 'O Pequeno Príncipe', autor: 'Antoine de Saint-Exupéry', ano: 1943, lido: false, categoria: 'Infantil' },
        { id: 3, titulo: '1984', autor: 'George Orwell', ano: 1949, lido: false, categoria: 'Ficção' }
      ],
      novoLivro: { titulo: '', autor: '', ano: new Date().getFullYear(), lido: false, categoria: 'Geral' }
    }
  },
  created() {
    console.log('App criado (created)')
  },
  mounted() {
    console.log('App montado (mounted)')
  },
  methods: {
    gerarId() {
      return Date.now() + Math.floor(Math.random()*1000)
    },
    adicionarLivro() {
      if (!this.novoLivro.titulo || !this.novoLivro.titulo.trim()) {
        alert('Título não pode ficar vazio')
        return
      }
      const novo = {
        id: this.gerarId(),
        titulo: this.novoLivro.titulo.trim(),
        autor: this.novoLivro.autor.trim() || 'Desconhecido',
        ano: Number(this.novoLivro.ano) || new Date().getFullYear(),
        lido: !!this.novoLivro.lido,
        categoria: this.novoLivro.categoria || 'Geral'
      }
      this.livros.push(novo)
      // limpar form
      this.novoLivro = { titulo: '', autor: '', ano: new Date().getFullYear(), lido: false, categoria: 'Geral' }
    },
    removerLivro(id) {
      if (confirm('Deseja remover o livro?')) {
        this.livros = this.livros.filter(l => l.id !== id)
      }
    },
    alternarLido(id) {
      const l = this.livros.find(x => x.id === id)
      if (l) l.lido = !l.lido
    }
  }
}
</script>

<style>
.app { font-family: Arial, sans-serif; margin: 20px; }
.grid { display:flex; gap:12px; flex-wrap:wrap; margin-top:12px; }
.form-add input { margin-bottom:6px; width:250px; }
</style>
'@ | Set-Content -Path .\src\App.vue -Encoding UTF8
