@'
<template>
  <article class="card" :class="{ lido: lido }">
    <h3>{{ titulo }}</h3>
    <p class="meta">{{ autor }} · {{ anoFormatado }}</p>
    <p class="categoria">{{ categoria }}</p>
    <div class="acoes">
      <button @click="emitToggle">{{ lido ? "Marcar como Não Lido" : "Marcar como Lido" }}</button>
      <button @click="emitRemover">Remover</button>
    </div>
  </article>
</template>

<script>
export default {
  name: 'CartaoLivro',
  props: {
    titulo: { type: String, required: true },
    autor: { type: String, required: true },
    ano: {
      type: Number,
      required: true,
      validator(value) {
        return typeof value === 'number' && value >= 1000 && value <= 2024
      }
    },
    lido: { type: Boolean, required: true },
    categoria: { type: String, default: 'Geral' }
  },
  computed: {
    anoFormatado() {
      return `Publicado em ${this.ano}`
    }
  },
  created() {
    console.log('CartaoLivro criado:', this.titulo)
  },
  mounted() {
    console.log('CartaoLivro montado:', this.titulo)
  },
  methods: {
    emitToggle() {
      this.$emit('toggle-lido', this.$props && this.$props.id ? this.$props.id : undefined)
      // Note: parent alterna pelo id passado nos handlers do template do App
    },
    emitRemover() {
      this.$emit('remover', this.$props && this.$props.id ? this.$props.id : undefined)
    }
  }
}
</script>

<style>
.card { border:1px solid #ccc; padding:10px; width:210px; border-radius:6px; background:#fff; }
.card.lido { background: #e6ffed; border-color:#8fd08f; }
.meta { color:#555; font-size:0.9rem; }
.acoes { margin-top:8px; display:flex; gap:8px; }
button { padding:6px 8px; cursor:pointer; }
</style>
'@ | Set-Content -Path .\src\components\CartaoLivro.vue -Encoding UTF8
