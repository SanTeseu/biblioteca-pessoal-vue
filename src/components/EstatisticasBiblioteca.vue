@'
<template>
  <div class="estat">
    <h4>Estatísticas</h4>
    <div>Total: <strong>{{ total }}</strong></div>
    <div>Lidos: <strong>{{ lidos }}</strong></div>
    <div>Não lidos: <strong>{{ naoLidos }}</strong></div>
    <div>Porcentagem lidos: <strong>{{ porcentagem }}%</strong></div>
    <div class="barra">
      <div class="progresso" :style="{ width: porcentagem + '%' }"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EstatisticasBiblioteca',
  props: {
    livros: { type: Array, required: true }
  },
  computed: {
    total() { return this.livros.length },
    lidos() { return this.livros.filter(l => l.lido).length },
    naoLidos() { return this.total - this.lidos },
    porcentagem() { return this.total ? Math.round((this.lidos / this.total) * 100) : 0 }
  },
  created() {
    console.log('EstatisticasBiblioteca criado')
  }
}
</script>

<style>
.barra { background:#eee; width:100%; height:12px; border-radius:6px; overflow:hidden; margin-top:6px; }
.progresso { height:100%; background:#4caf50; width:0%; }
.estat { border:1px dashed #ccc; padding:8px; margin:10px 0; border-radius:6px; }
</style>
'@ | Set-Content -Path .\src\components\EstatisticasBiblioteca.vue -Encoding UTF8
