<script setup lang="ts">
defineProps<{
  size?: 'small' | 'normal'
}>()
</script>

<template>
  <div class="logo" :class="size">
    <img src="@/assets/logo.png" alt="AI智绘伴读" />
    <span class="logo-text">AI智绘伴读</span>
  </div>
</template>

<style lang="scss" scoped>
.logo {
  display: flex;
  align-items: center;
  gap: 8px;
  
  img {
    height: 32px;
    border-radius: 50%;
  }

  &.small img {
    height: 24px;
  }

  .logo-text {
    font-size: 18px;
    font-weight: 500;
  }
}
</style> 