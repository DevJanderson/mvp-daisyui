# MVP DaisyUI

Projeto Vue 3 com DaisyUI, Tailwind CSS e auto-import configurado.

## Stack

- **Vue 3** - Framework JavaScript
- **Vite** - Build tool
- **Tailwind CSS v4** - Framework CSS utilitario
- **DaisyUI** - Componentes UI para Tailwind
- **Vue Router** - Roteamento SPA
- **ESLint + Prettier** - Linting e formatacao

## Auto-Import

O projeto utiliza plugins para auto-import, eliminando a necessidade de imports manuais.

### APIs (unplugin-auto-import)

Funcoes do Vue e Vue Router sao importadas automaticamente:

```vue
<script setup>
// Nao precisa importar!
const count = ref(0)
const doubled = computed(() => count.value * 2)
const router = useRouter()
const route = useRoute()

onMounted(() => {
  console.log('Montado!')
})
</script>
```

**APIs disponiveis:**
- Vue: `ref`, `reactive`, `computed`, `watch`, `watchEffect`, `onMounted`, `onUnmounted`, etc.
- Vue Router: `useRouter`, `useRoute`, `onBeforeRouteLeave`, `onBeforeRouteUpdate`

### Componentes (unplugin-vue-components)

Componentes das pastas `src/components` e `src/layouts` sao registrados automaticamente:

```vue
<template>
  <!-- Nao precisa importar DefaultLayout! -->
  <DefaultLayout>
    <MyComponent />
  </DefaultLayout>
</template>
```

**Pastas escaneadas:**
- `src/components` - Componentes reutilizaveis
- `src/layouts` - Layouts de pagina

## Estrutura do Projeto

```
src/
├── assets/          # Arquivos estaticos (CSS, imagens)
│   └── main.css     # Estilos globais + Tailwind
├── components/      # Componentes Vue (auto-import)
├── layouts/         # Layouts de pagina (auto-import)
│   └── DefaultLayout.vue
├── pages/           # Paginas/Views
│   ├── HomeView.vue
│   └── AboutView.vue
├── router/          # Configuracao de rotas
│   └── index.js
├── App.vue          # Componente raiz
└── main.js          # Entry point
```

## Scripts

```bash
# Desenvolvimento
npm run dev

# Build para producao
npm run build

# Preview do build
npm run preview

# Linting
npm run lint

# Formatacao
npm run format
```

## Arquivos Gerados (nao editar)

Estes arquivos sao gerados automaticamente pelos plugins:

- `auto-imports.d.ts` - Tipos para APIs auto-importadas
- `components.d.ts` - Tipos para componentes auto-importados
- `.eslintrc-auto-import.json` - Globals para ESLint

## DaisyUI

Componentes DaisyUI estao disponiveis via classes CSS:

```vue
<template>
  <!-- Botoes -->
  <button class="btn">Default</button>
  <button class="btn btn-primary">Primary</button>

  <!-- Input -->
  <input type="text" class="input input-bordered" />

  <!-- Card -->
  <div class="card bg-base-100 shadow-xl">
    <div class="card-body">
      <h2 class="card-title">Titulo</h2>
      <p>Conteudo</p>
    </div>
  </div>

  <!-- Navbar -->
  <div class="navbar bg-base-100">
    <a class="btn btn-ghost text-xl">Logo</a>
  </div>
</template>
```

Documentacao completa: https://daisyui.com/components/

## Configuracao do Vite

O arquivo `vite.config.js` inclui:

- `@vitejs/plugin-vue` - Suporte a Vue SFC
- `vite-plugin-vue-devtools` - DevTools integrado
- `@tailwindcss/vite` - Tailwind CSS v4
- `unplugin-auto-import` - Auto-import de APIs
- `unplugin-vue-components` - Auto-import de componentes

## IDE Recomendada

[VS Code](https://code.visualstudio.com/) + [Vue (Official)](https://marketplace.visualstudio.com/items?itemName=Vue.volar)

## Setup do Navegador

- Chromium (Chrome, Edge, Brave): [Vue.js devtools](https://chromewebstore.google.com/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)
- Firefox: [Vue.js devtools](https://addons.mozilla.org/en-US/firefox/addon/vue-js-devtools/)
