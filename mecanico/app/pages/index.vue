
<script setup lang="ts">
import { ref } from 'vue'

useHead({
  title: 'MotoTech | Mecânica de Motocicletas'
})

const menuAberto = ref(false)

const conteudos = [
  {
    titulo: 'Dicas de Mecânica',
    descricao: 'Aprenda sobre manutenção e reparos.',
    icone: '🔧',
    link: '/dicas'
  },
  {
    titulo: 'Biblioteca Técnica',
    descricao: 'Apostilas e manuais de motocicletas.',
    icone: '📚',
    link: '/biblioteca'
  },
  {
    titulo: 'Videoaulas',
    descricao: 'Aulas práticas de mecânica.',
    icone: '▶️',
    link: '/videos'
  },
  {
    titulo: 'Galeria de Fotos',
    descricao: 'Fotos de serviços e projetos.',
    icone: '📷',
    link: '/galeria'
  }
]
</script>

<template>
  <div class="site">
    <header class="cabecalho">
      <div class="container barra">
        <NuxtLink to="/" class="logo">
          <span class="logo-icone">🔧</span>
          <span>MotoTech</span>
        </NuxtLink>

        <button
          class="menu-botao"
          type="button"
          aria-label="Abrir ou fechar menu"
          :aria-expanded="menuAberto"
          @click="menuAberto = !menuAberto"
        >
          ☰
        </button>

        <nav :class="['navegacao', { aberta: menuAberto }]">
          <NuxtLink to="/">Início</NuxtLink>
          <NuxtLink to="/dicas">Dicas</NuxtLink>
          <NuxtLink to="/biblioteca">Biblioteca</NuxtLink>
          <NuxtLink to="/videos">Vídeos</NuxtLink>
          <NuxtLink to="/galeria">Galeria</NuxtLink>
        </nav>
      </div>
    </header>

    <main>
      <section class="hero">
        <div class="container">
          <span class="etiqueta">MECÂNICA DE MOTOCICLETAS</span>
          <h1>"Conhecimento que move você, meu filho".</h1>
          <p>
            Aprenda mecânica com dicas, videoaulas,
            manuais técnicos e conteúdos práticos.
          </p>

          <a href="#conteudos" class="botao-principal">
            Explorar conteúdos →
          </a>
        </div>
      </section>

      <section id="conteudos" class="secao container">
        <div class="secao-titulo">
          <h2>Explore nossos conteúdos</h2>
          <p>Escolha por onde deseja começar.</p>
        </div>

        <div class="grade-cartoes">
          <NuxtLink
            v-for="item in conteudos"
            :key="item.titulo"
            :to="item.link"
            class="cartao"
          >
            <div class="cartao-icone">{{ item.icone }}</div>
            <h3>{{ item.titulo }}</h3>
            <p>{{ item.descricao }}</p>
            <span class="cartao-link">Saiba mais →</span>
          </NuxtLink>
        </div>
      </section>
    </main>

    <footer class="rodape">
      © 2026 MotoTech — Mecânica de Motocicletas
    </footer>
  </div>
</template>
