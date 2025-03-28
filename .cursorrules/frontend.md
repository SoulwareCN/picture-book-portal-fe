# 前端项目开发规范文档

## 0. 框架和依赖规范

### 0.1 核心框架版本
```json
{
  "vue": "^3.4.0",
  "vue-router": "^4.2.0",
  "pinia": "^2.1.0",
  "typescript": "^5.0.0"
}
```

### 0.2 UI 组件库
```json
{
  "element-plus": "^2.4.0",
  "@element-plus/icons-vue": "^2.1.0"
}
```

### 0.3 工具库
```json
{
  "axios": "^1.6.0",
  "lodash-es": "^4.17.21",
  "dayjs": "^1.11.0"
}
```

### 0.4 开发工具
```json
{
  "vite": "^5.0.0",
  "eslint": "^8.0.0",
  "prettier": "^3.0.0",
  "sass": "^1.69.0"
}
```

### 0.5 依赖管理规范
1. 版本锁定
   - 使用 `package-lock.json` 或 `yarn.lock` 锁定依赖版本
   - 禁止使用 `*` 或 `latest` 等不确定版本

2. 版本更新
   - 定期更新依赖包到最新的稳定版本
   - 更新前需要在开发环境充分测试
   - 重大版本更新需要团队讨论决定

3. 依赖选择原则
   - 选择社区活跃、文档完善的依赖包
   - 优先使用官方推荐的依赖包
   - 考虑包的体积和性能影响

4. 依赖安装规范
   - 开发依赖使用 `devDependencies`
   - 运行时依赖使用 `dependencies`
   - 禁止全局安装项目依赖

## 1. 项目结构规范

```
src/
├── api/                # API 接口定义
│   ├── types/         # API 相关类型定义
│   └── config.ts      # API 配置（baseURL、拦截器等）
├── assets/            # 静态资源
├── components/        # 公共组件
├── router/            # 路由配置
├── utils/            # 工具函数
├── views/            # 页面组件
└── App.vue           # 根组件
```

## 2. 组件开发规范

### 2.1 组件文件命名
- 使用 PascalCase 命名组件文件，如：`PictureEditor.vue`
- 页面组件放在 views 目录下，如：`Home.vue`
- 公共组件放在 components 目录下

### 2.2 组件结构
```vue
<script setup lang="ts">
// 1. 导入声明
import { ref, computed } from 'vue'
import type { PropType } from 'vue'

// 2. Props 定义
const props = defineProps<{
  propName: PropType<Type>
}>()

// 3. Emits 定义
const emit = defineEmits<{
  'event-name': [param: Type]
}>()

// 4. 响应式数据
const data = ref<Type>()

// 5. 计算属性
const computed = computed(() => {})

// 6. 方法定义
const handleEvent = () => {}

// 7. 生命周期钩子
onMounted(() => {})
</script>

<template>
  <div class="component-name">
    <!-- 模板内容 -->
  </div>
</template>

<style lang="scss" scoped>
.component-name {
  // 样式定义
}
</style>
```

### 2.3 组件拆分原则
- 单一职责：每个组件只负责一个功能
- 可复用性：提取可复用的逻辑为独立组件
- 适当粒度：避免组件过大，建议超过 500 行就考虑拆分

## 3. TypeScript 规范

### 3.1 类型定义
- 使用 interface 定义对象类型
- 使用 type 定义联合类型或工具类型
- 类型定义文件放在对应模块的 types 目录下

```typescript
// API 响应类型
interface ApiResponse<T> {
  code: number
  message: string
  data: T
}

// 组件 Props 类型
interface ComponentProps {
  prop1: string
  prop2?: number
}
```

### 3.2 类型注解
- 始终为函数参数和返回值添加类型注解
- 使用 type 或 interface 而不是 any
- 合理使用泛型增加代码复用性

## 4. 样式规范

### 4.1 CSS 命名规范
- 使用 kebab-case 命名 class
- 使用 BEM 命名方法论
- 组件最外层 class 使用组件名

```scss
.component-name {
  &__element {
    // 元素样式
  }

  &--modifier {
    // 修饰符样式
  }
}
```

### 4.2 响应式设计
- 使用 media query 实现响应式
- 移动端优先的设计理念
- 断点设置：
  ```scss
  // 移动端
  @media screen and (max-width: 768px) {
    // 样式
  }
  
  // 平板
  @media screen and (max-width: 1024px) {
    // 样式
  }
  ```

## 5. API 接口规范

### 5.1 接口定义
```typescript
// api/types/module.ts
interface RequestParams {
  // 请求参数类型
}

interface ResponseData {
  // 响应数据类型
}

// api/module.ts
export const apiFunction = async (params: RequestParams): Promise<ResponseData> => {
  return request.post('/endpoint', params)
}
```

### 5.2 错误处理
- 统一的错误处理机制
- 使用 try-catch 处理异步操作
- 友好的错误提示

## 6. 代码质量规范

### 6.1 命名规范
- 变量：使用 camelCase
- 常量：使用 UPPER_SNAKE_CASE
- 组件：使用 PascalCase
- 文件：使用 PascalCase（组件）或 kebab-case（其他）

### 6.2 注释规范
- 组件顶部添加功能说明
- 复杂逻辑添加必要的注释
- 使用 JSDoc 注释格式

```typescript
/**
 * 组件描述
 * @param {Type} prop - 参数描述
 * @returns {Type} 返回值描述
 */
```

### 6.3 代码格式化
- 使用 ESLint 进行代码检查
- 使用 Prettier 进行代码格式化
- 提交前进行代码检查

## 7. 性能优化规范

### 7.1 代码分割
- 路由懒加载
- 组件按需加载
- 第三方库按需导入

### 7.2 资源优化
- 图片资源压缩
- 使用 CDN 加载第三方库
- 合理使用缓存策略

## 8. 版本控制规范

### 8.1 Git 提交规范
```
feat: 新功能
fix: 修复问题
docs: 文档修改
style: 代码格式修改
refactor: 代码重构
perf: 性能优化
test: 测试相关
chore: 构建过程或辅助工具的变动
```

### 8.2 分支管理
- main：主分支
- develop：开发分支
- feature/*：功能分支
- hotfix/*：紧急修复分支

## 9. 安全规范

### 9.1 数据安全
- 敏感数据加密存储
- API 请求使用 HTTPS
- 防止 XSS 和 CSRF 攻击

### 9.2 权限控制
- 路由权限控制
- API 权限控制
- 按钮级别权限控制 