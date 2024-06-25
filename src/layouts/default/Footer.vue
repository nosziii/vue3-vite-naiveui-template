<template>
  <n-layout-footer>
    <n-p>
      Made with <n-text type="error">♥</n-text> by
      <n-a href="https://github.com/noszii">Noszii</n-a>. Licensed under
      the MIT License.
    </n-p>
    <n-p
      >&copy; {{ new Date().getFullYear() }} Noszii. All rights reserved.</n-p
    >
  </n-layout-footer>
</template>

<style scoped>
.n-layout-footer {
  opacity: 0.6;
  padding: 30px;
  text-align: center;
}
.n-a {
  text-decoration: none;
}
</style>
