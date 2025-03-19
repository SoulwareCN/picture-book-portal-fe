<script setup lang="ts">
import Logo from './Logo.vue'
import { ref } from 'vue'

const navItems = [
  { text: '首页', link: '/' },
  { text: '功能特点', link: '/#features' },
  { text: '应用截图', link: '/#preview' },
  { text: '立即下载', link: '/#download' },
  { text: '联系我们', link: '/#contact' }
]

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<template>
  <header class="header">
    <div class="header-content">
      <Logo />
      <button class="menu-btn" @click="toggleMenu">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <nav class="nav" :class="{ 'is-open': isMenuOpen }">
        <a v-for="item in navItems" 
           :key="item.text" 
           :href="item.link"
           @click="closeMenu"
           class="nav-item">
          {{ item.text }}
        </a>
      </nav>
    </div>
  </header>
</template>

<style lang="scss" scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 64px;
  background: rgba(255, 255, 255, 0.98);
  backdrop-filter: blur(5px);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  z-index: 1000;

  .header-content {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .nav {
    display: flex;
    gap: 32px;
    position: relative;
    z-index: 1100;

    .nav-item {
      color: var(--text-color);
      font-size: 16px;
      transition: color 0.2s;

      &:hover {
        color: var(--primary-color);
      }
    }
  }
}

.menu-btn {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 24px;
  height: 20px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0;
  position: relative;
  z-index: 1200;

  span {
    display: block;
    width: 100%;
    height: 2px;
    background: var(--text-color);
    transition: all 0.3s;
  }
}

@media screen and (max-width: 768px) {
  .header {
    height: 56px;

    .header-content {
      padding: 0 16px;
      position: relative;
    }

    .nav {
      display: none;
    }
  }

  .menu-btn {
    display: none;
    margin-right: -8px;
  }
}
</style> 