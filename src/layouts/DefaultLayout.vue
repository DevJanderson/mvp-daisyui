<script setup>
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <!-- Header -->
    <header>
      <div class="navbar bg-base-100 shadow-sm">
        <div class="flex-1">
          <a class="btn btn-ghost text-xl">MCP-DaisyUI</a>
        </div>
        <div class="flex-none">
          <ul class="menu menu-horizontal px-1">
            <li><a>Home</a></li>
          </ul>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <main class="flex-1">
      <slot />
    </main>

    <!-- Footer -->
    <footer>
      <!-- Cole aqui o código do footer do DaisyUI -->
    </footer>
  </div>
</template>
