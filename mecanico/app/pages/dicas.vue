
<script setup lang="ts">
type Dica = {
  id: number
  titulo: string
  categoria: string
  descricao: string
}

useHead({
  title: 'Dicas de Mecânica | MotoTech'
})

const {
  data: dicas,
  status,
  error,
  refresh
} = await useFetch<Dica[]>('/api/dicas', {
  default: () => []
})
</script>

<template>
  <main class="pagina-dicas">
    <div class="conteudo">
      <NuxtLink to="/" class="voltar">
        ← Voltar ao início
      </NuxtLink>

      <h1>Dicas de Mecânica</h1>
      <p class="introducao">
        Conheça dicas e orientações para manutenção
        de motocicletas.
      </p>

      <p v-if="status === 'pending'">
        Carregando dicas...
      </p>

      <div v-else-if="error" class="erro">
        <p>Não foi possível carregar as dicas.</p>
        <button @click="refresh()">
          Tentar novamente
        </button>
      </div>

      <p v-else-if="!dicas?.length">
        Nenhuma dica cadastrada.
      </p>

      <div v-else class="grade">
        <article
          v-for="dica in dicas"
          :key="dica.id"
          class="cartao-dica"
        >
          <span class="categoria">
            {{ dica.categoria }}
          </span>

          <h2>{{ dica.titulo }}</h2>
          <p>{{ dica.descricao }}</p>
        </article>
      </div>
    </div>
  </main>
</template>

<style scoped>
.pagina-dicas {
  min-height: 100vh;
  background: #f5f9ff;
  padding: 60px 20px;
}

.conteudo {
  max-width: 1120px;
  margin: 0 auto;
}

.voltar {
  color: #1558a6;
  font-weight: 600;
}

h1 {
  color: #0b3265;
  font-size: 38px;
  margin-top: 35px;
}

.introducao {
  color: #647b95;
  margin-bottom: 35px;
}

.grade {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 22px;
}

.cartao-dica {
  background: #ffffff;
  border: 1px solid #dce8f6;
  border-radius: 14px;
  padding: 28px;
  box-shadow: 0 5px 15px #1558a60d;
}

.categoria {
  display: inline-block;
  background: #e9f2ff;
  color: #1558a6;
  padding: 7px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 700;
}

.cartao-dica h2 {
  color: #0b3265;
  margin-top: 20px;
}

.cartao-dica p {
  color: #647b95;
  line-height: 1.7;
}

.erro {
  color: #9c2525;
}

.erro button {
  padding: 10px 16px;
  cursor: pointer;
}

@media (max-width: 640px) {
  .grade {
    grid-template-columns: 1fr;
  }
}
</style>
