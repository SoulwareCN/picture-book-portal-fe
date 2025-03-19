<script setup lang="ts">
import { ref } from 'vue'
import type { Feature, AppStats } from '../types'
import Header from '@/components/Header.vue'

const features = ref<Feature[]>([
  {
    icon: '📚',
    title: '便捷导入绘本',
    description: '支持拍照上传或PDF导入绘本，AI快速精准识别内容，让家长轻松开启亲子阅读时光'
  },
  {
    icon: '🤖',
    title: 'AI智能陪读',
    description: '先进AI算法智能解析绘本内容，以自然语音进行生动陪读，营造沉浸式阅读体验'
  },
  {
    icon: '🎯',
    title: '互动点读发音',
    description: '支持句子和单字精准发音，帮助孩子感受语言韵律，纠正发音偏差'
  },
  {
    icon: '💭',
    title: 'AI智能对话',
    description: '孩子可以通过语音与AI进行深度对话交流，探讨故事情节，激发思维能力'
  },
  {
    icon: '🎨',
    title: '个性化体验',
    description: '根据每个孩子的阅读习惯和需求提供定制化服务，真正实现因材施教'
  }
])

const stats = ref<AppStats>({
  downloads: '50万+',
  rating: '4.8',
  books: '1000+'
})

const socialLinks = [
  { icon: 'weibo', link: '#' },
  { icon: 'wechat', link: '#' },
  { icon: 'email', link: 'mailto:soulware_ddl_mini@163.com' }
]

const scrollToDownload = () => {
  const downloadSection = document.getElementById('download')
  downloadSection?.scrollIntoView({ behavior: 'smooth' })
}

const appStoreUrl = 'https://apps.apple.com/cn/app/%E5%8A%A8%E7%89%A9%E6%80%8E%E4%B9%88%E5%8F%AB/id6741844116'
const googlePlayUrl = 'https://play.google.com/store/apps/details?id=com.animalvoice'

const showQRCode = ref(false)
const showDevTip = ref(false)

const toggleQRCode = () => {
  showQRCode.value = !showQRCode.value
}

const showDevTipMessage = () => {
  showDevTip.value = true
  setTimeout(() => {
    showDevTip.value = false
  }, 3000)
}
</script>

<template>
  <div class="home">
    <Header />
    
    <!-- 头部区域 -->
    <header class="hero">
      <div class="hero-content">
        <h1>让孩子爱上绘本阅读的AI助手</h1>
        <p>智能陪读、互动点读、AI对话，打造沉浸式亲子阅读体验</p>
        <div class="cta-buttons">
          <button class="download-btn" @click="scrollToDownload">立即下载</button>
        </div>
      </div>
    </header>

    <!-- 特色功能区域 -->
    <section class="features" id="features">
      <h2>特色功能</h2>
      <div class="feature-grid">
        <div v-for="feature in features" 
             :key="feature.title" 
             class="feature-card">
          <div class="feature-icon">{{ feature.icon }}</div>
          <h3>{{ feature.title }}</h3>
          <p>{{ feature.description }}</p>
        </div>
      </div>
    </section>

    <!-- 应用界面展示 -->
    <section class="app-preview" id="preview">
      <h2>应用界面</h2>
      <div class="preview-images">
        <div class="preview-item">
          <img src="@/assets/preview-1.png" alt="绘本导入" />
          <p>便捷导入绘本</p>
        </div>
        <div class="preview-item">
          <img src="@/assets/preview-2.png" alt="智能陪读" />
          <p>AI智能陪读</p>
        </div>
        <div class="preview-item">
          <img src="@/assets/preview-3.png" alt="互动点读" />
          <p>互动点读发音</p>
        </div>
      </div>
    </section>

    <!-- 下载区域 -->
    <section class="download" id="download">
      <h2>立即下载体验</h2>
      <div class="download-buttons">
        <a @click.prevent="showDevTipMessage" 
           class="app-store">
          <img src="@/assets/app-store.svg" alt="App Store" />
          App Store 下载
        </a>
        <div class="miniapp-btn" 
             @click="showDevTipMessage">
          <img src="@/assets/wechat.svg" alt="微信小程序" />
          小程序版本
        </div>
      </div>

      <!-- 开发中提示 -->
      <div class="dev-tip" v-show="showDevTip">
        应用正在开发中，敬请期待！
      </div>

      <!-- <div class="stats">
        <div class="stat-item">
          <h3>{{ stats.downloads }}</h3>
          <p>累计下载</p>
        </div>
        <div class="stat-item">
          <h3>{{ stats.rating }}</h3>
          <p>用户评分</p>
        </div>
        <div class="stat-item">
          <h3>{{ stats.books }}</h3>
          <p>支持绘本</p>
        </div>
      </div> -->
    </section>

    <!-- 联系我们 -->
    <section class="contact" id="contact">
      <h2>联系我们</h2>
      <p>如果您有任何问题或建议，欢迎随时与我们联系</p>
      <p class="email">客服邮箱：soulware_ddl_mini@163.com</p>
    </section>

    <!-- 页脚 -->
    <footer class="footer">
      <div class="footer-content">
        <div class="copyright">
          © 2025 魂技点读宝 保留所有权利
        </div>
      </div>
    </footer>
  </div>
</template>

<style lang="scss" scoped>
@use "sass:color";

.home {
  padding-top: 64px; // 为固定导航栏留出空间
}

.hero {
  position: relative;
  padding: 80px 0;
  overflow: hidden;
  background: url(/src/assets/hero-animals.png?t=1739251843457);
  background-position: center bottom;
  background-repeat: no-repeat;
  background-size: cover;

  .hero-content {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    position: relative;
    z-index: 1;
  }

  h1 {
    font-size: 2.5rem;
    margin-bottom: 20px;
    color: var(--text-color);
  }

  p {
    font-size: 1.2rem;
    color: #666;
    margin-bottom: 40px;
  }

  .hero-image {
    position: absolute;
    right: 50%;
    bottom: 0;
    width: 50%;
    max-width: 600px;
  }
}

.cta-buttons {
  display: flex;
  gap: 20px;

  button {
    padding: 12px 30px;
    border-radius: 25px;
    font-size: 1.1rem;
    cursor: pointer;
    transition: all 0.3s;
  }

  .download-btn {
    background: var(--primary-color);
    color: white;
    border: none;

    &:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(255, 107, 107, 0.3);
    }
  }

  .preview-btn {
    background: white;
    border: 2px solid var(--primary-color);
    color: var(--primary-color);

    &:hover {
      background: var(--primary-color);
      color: white;
    }
  }
}

.features {
  padding: 80px 0;
  background: white;

  h2 {
    text-align: center;
    margin-bottom: 50px;
    color: var(--text-color);
  }

  .feature-grid {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
  }

  .feature-card {
    text-align: center;
    padding: 30px;
    border-radius: 10px;
    background: white;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s;

    &:hover {
      transform: translateY(-5px);
    }

    .feature-icon {
      font-size: 2.5rem;
      margin-bottom: 20px;
    }

    h3 {
      margin-bottom: 15px;
      color: var(--text-color);
    }

    p {
      color: #666;
      line-height: 1.6;
    }
  }
}

.app-preview {
  padding: 80px 0;
  text-align: center;
  background: white;

  h2 {
    margin-bottom: 40px;
  }

  .preview-images {
    display: flex;
    gap: 20px;
    justify-content: center;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scroll-padding-left: 20px;
    
    &::-webkit-scrollbar {
      display: none;
    }
    
    .preview-item {
      flex: 0 0 280px;
      
      img {
        width: 100%;
        height: 500px;
        object-fit: cover;
        border-radius: 20px;
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        transition: transform 0.3s;
        
        &:hover {
          transform: translateY(-5px);
        }
      }
      
      p {
        margin-top: 12px;
        font-size: 16px;
        color: var(--text-color);
      }
    }
  }
}

.download {
  padding: 80px 0;
  text-align: center;
  background: white;

  h2 {
    margin-bottom: 50px;
    color: var(--text-color);
  }

  .download-buttons {
    display: flex;
    gap: 20px;
    justify-content: center;
    margin-bottom: 60px;

    a {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 12px 30px;
      border-radius: 25px;
      font-weight: bold;
      transition: all 0.3s;

      img {
        height: 24px;
      }
    }

    .app-store {
      background: #000;
      color: white;

      &:hover {
        background: #333;
      }
    }

    .google-play {
      background: var(--primary-color);
      color: white;

      &:hover {
        background: color.adjust(#ff6b6b, $lightness: -10%);
      }
    }

    .miniapp-btn {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 12px 30px;
      border-radius: 25px;
      font-weight: bold;
      transition: all 0.3s;
      background: #07c160; // 微信绿色
      color: white;
      cursor: pointer;
      position: relative; // 为弹出层定位

      img {
        height: 24px;
      }

      &:hover {
        background: color.adjust(#07c160, $lightness: -10%);
      }

      .qrcode-popup {
        position: absolute;
        bottom: 100%;
        left: 50%;
        transform: translateX(-50%);
        margin-bottom: 15px;
        padding: 15px;
        background: white;
        border-radius: 8px;
        box-shadow: 0 5px 20px rgba(0, 0, 0, 0.15);
        text-align: center;
        width: 200px;
        
        &::after {
          content: '';
          position: absolute;
          top: 100%;
          left: 50%;
          transform: translateX(-50%);
          border-width: 8px;
          border-style: solid;
          border-color: white transparent transparent transparent;
        }

        img {
          width: 160px;
          height: 160px;
          margin-bottom: 10px;
        }

        p {
          color: #666;
          font-size: 14px;
          margin: 0;
        }
      }
    }
  }
}

.stats {
  display: flex;
  justify-content: center;
  gap: 60px;

  .stat-item {
    text-align: center;

    h3 {
      font-size: 2rem;
      color: var(--primary-color);
      margin-bottom: 10px;
    }

    p {
      color: #666;
    }
  }
}

.contact {
  padding: 80px 0;
  text-align: center;
  background: var(--bg-color);

  h2 {
    margin-bottom: 20px;
    color: var(--text-color);
  }

  p {
    color: #666;
    margin-bottom: 30px;
  }

  .social-links {
    display: flex;
    justify-content: center;
    gap: 30px;
    margin-bottom: 30px;

    .social-link {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background: white;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: transform 0.3s;

      &:hover {
        transform: translateY(-3px);
      }

      img {
        width: 24px;
        height: 24px;
      }
    }
  }

  .email {
    color: #666;
  }
}

.footer {
  padding: 20px 0;
  background: white;
  border-top: 1px solid #eee;

  .footer-content {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    text-align: center;
    color: #666;
  }
}

@media screen and (max-width: 768px) {
  .hero {
    text-align: center;
    padding: 40px 0;
    background-size: cover;
    background-position: right;
    min-height: 480px;
    display: flex;
    align-items: center;
    justify-content: center;

    h1 {
      font-size: 1.8rem;
      margin-bottom: 15px;
      padding: 0 20px;
    }

    p {
      font-size: 1rem;
      margin-bottom: 30px;
      padding: 0 20px;
    }

    .cta-buttons {
      flex-direction: column;
      align-items: center;
      gap: 15px;
      padding: 0 20px;

      button {
        width: 100%;
        max-width: 280px;
        height: 48px;
        font-size: 1rem;
      }
    }
  }

  .features {
    padding: 40px 0;

    h2 {
      font-size: 1.6rem;
      margin-bottom: 30px;
    }

    .feature-grid {
      grid-template-columns: 1fr;
      gap: 20px;
      padding: 0 20px;
    }

    .feature-card {
      padding: 24px 20px;
      margin: 0 12px;

      .feature-icon {
        font-size: 2rem;
        margin-bottom: 16px;
      }

      h3 {
        font-size: 1.2rem;
        margin-bottom: 12px;
      }

      p {
        font-size: 0.9rem;
        line-height: 1.5;
      }
    }
  }

  .app-preview {
    padding: 40px 0;

    h2 {
      font-size: 1.6rem;
      margin-bottom: 30px;
    }

    .preview-images {
      gap: 12px;
      padding-left: 20px;
      padding-right: 20px;
      margin: 0;
      justify-content: flex-start;
      
      .preview-item {
        flex: 0 0 220px;
        
        img {
          height: 380px;
          border-radius: 16px;
        }

        p {
          font-size: 0.9rem;
          margin-top: 8px;
        }
      }
    }
  }

  .download {
    padding: 40px 0;

    h2 {
      font-size: 1.6rem;
      margin-bottom: 30px;
    }

    .download-buttons {
      flex-direction: column;
      align-items: center;
      gap: 15px;
      margin-bottom: 30px;
      padding: 0 20px;

      a, .miniapp-btn {
        width: 100%;
        max-width: 280px;
        justify-content: center;
        height: 48px;
        font-size: 1rem;
      }

      img {
        height: 20px;
      }
    }

    .miniapp-btn {
      .qrcode-popup {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        margin: 0;
        z-index: 1000;
        width: 90%;
        max-width: 280px;
        background: rgba(255, 255, 255, 0.98);
        backdrop-filter: blur(10px);
        
        &::after {
          display: none;
        }

        img {
          width: 100%;
          height: auto;
          max-width: 200px;
          margin: 0 auto 10px;
        }

        p {
          font-size: 0.9rem;
          color: #666;
        }
      }
    }
  }

  .contact {
    padding: 40px 0;

    h2 {
      font-size: 1.5rem;
      margin-bottom: 15px;
    }

    p {
      font-size: 0.9rem;
      margin-bottom: 20px;
      padding: 0 20px;
    }

    .email {
      word-break: break-all;
      padding: 0 20px;
    }
  }

  .footer {
    padding: 15px 0;

    .footer-content {
      font-size: 0.9rem;
      padding: 0 20px;
    }
  }

  @media screen and (orientation: landscape) {
    .hero {
      min-height: auto;
      padding: 30px 0;
      background-size: 60% auto;
    }

    .app-preview .preview-images .preview-item {
      flex: 0 0 180px;
      
      img {
        height: 320px;
      }
    }
  }
}

.animal-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr); /* 默认手机端两列 */
  gap: 16px;
  padding: 16px;
}

/* iPad 竖屏 - 最小宽度768px */
@media (min-width: 768px) {
  .animal-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}

/* iPad 横屏 - 最小宽度1024px */
@media (min-width: 1024px) {
  .animal-grid {
    grid-template-columns: repeat(6, 1fr);
  }
}

.animal-card {
  // ... 现有样式保持不变 ...
}

.dev-tip {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 15px 30px;
  border-radius: 25px;
  font-size: 16px;
  z-index: 1000;
  animation: fadeInOut 3s ease-in-out;
}

@keyframes fadeInOut {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.9);
  }
  20% {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
  80% {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
  100% {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.9);
  }
}

.download-buttons {
  .app-store, .miniapp-btn {
    cursor: pointer;
  }
}
</style> 