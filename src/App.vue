<template>
  <main>
    <HomePage />
  </main>
</template>

<script setup lang="ts" >
import HomePage from '@/pages/HomePage.vue' 
</script>

<style lang="scss">
:root {
  --color-primary: #ff00ff;
  --color-primary-light: #ff2a6d;
  --color-primary-dark: #cc00cc;
  --color-background: #0f0f1b;      
  --color-surface: #1a1a2e;        
  --color-disabled: #2a2a3d;

  --color-text: #f0f0ff;
  --color-text-muted: #a0a0c0;
  --color-placeholder: #8a8ab3;

  --color-border: #393953;


  --color-success: #00f0a0;       
  --color-error: #ff2a6d;          
  --color-warning: #ffaa00;       
  --color-info: #4dccff;           

  --color-focus: rgba(255, 0, 255, 0.4);
  --color-primary-glow: rgba(255, 0, 255, 0.6);
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Ubuntu', sans-serif;
  color: var(--color-text);
  background-color: var(--color-background);
  min-height: 100vh;
  overflow-x: hidden;
}
</style>