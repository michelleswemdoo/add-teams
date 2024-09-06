<template>
  <header class="header">
    <div class="header-container">
      <h1>Logo</h1>
    </div>
  </header>
</template>

<script setup lang="ts"></script>

<style scoped>
.header {
  position: sticky;
  inset: 0;
  width: 100%;
  z-index: 999;
  background-color: #fff;
}

.header-container {
  text-align: center;
  padding: 8px 24px;
}

h1 {
  font-size: 18px;
  font-weight: 600;
  color: #be185d;
  line-height: 28px;
}
</style>
