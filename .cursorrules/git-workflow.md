# Git 工作流规范

## 1. 分支管理

### 1.1 分支命名
- `main`: 主分支，用于生产环境
- `develop`: 开发分支，用于开发环境
- `feature/*`: 功能分支，用于开发新功能
- `hotfix/*`: 紧急修复分支，用于修复生产环境问题
- `release/*`: 发布分支，用于版本发布

### 1.2 分支命名规范
- 功能分支：`feature/功能名称`，如 `feature/user-login`
- 修复分支：`hotfix/问题描述`，如 `hotfix/login-error`
- 发布分支：`release/版本号`，如 `release/v1.0.0`

## 2. 提交规范

### 2.1 提交信息格式
```
<type>(<scope>): <subject>

<body>

<footer>
```

### 2.2 Type 类型
- `feat`: 新功能
- `fix`: 修复问题
- `docs`: 文档修改
- `style`: 代码格式修改，不影响代码逻辑
- `refactor`: 代码重构
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建过程或辅助工具的变动

### 2.3 Scope 范围
- 表示 commit 影响的范围
- 可以是具体的功能模块
- 如果影响多个模块，可以使用 * 

### 2.4 Subject 描述
- 简短描述，不超过 50 个字符
- 使用第一人称现在时态
- 第一个字母小写
- 结尾不加句号

### 2.5 Body 正文
- 详细描述改动原因和改动点
- 可以分多行
- 每行不超过 72 个字符

### 2.6 Footer 页脚
- 关闭 Issue：`Closes #123, #456`
- Breaking Changes 破坏性变更说明

### 2.7 示例
```
feat(auth): implement user login functionality

- Add login form component
- Implement login API integration
- Add token management
- Add user session handling

Closes #123
```

## 3. 工作流程

### 3.1 功能开发
1. 从 `develop` 分支创建功能分支
2. 在功能分支上进行开发
3. 提交代码，遵循提交规范
4. 创建 Pull Request 到 `develop` 分支
5. Code Review 通过后合并

### 3.2 紧急修复
1. 从 `main` 分支创建 hotfix 分支
2. 在 hotfix 分支上修复问题
3. 提交代码，遵循提交规范
4. 创建 Pull Request 到 `main` 和 `develop` 分支
5. Code Review 通过后合并

### 3.3 版本发布
1. 从 `develop` 分支创建 release 分支
2. 在 release 分支上进行测试和 bug 修复
3. 测试通过后，合并到 `main` 和 `develop` 分支
4. 在 `main` 分支上打 tag

## 4. Code Review

### 4.1 Review 重点
- 代码规范性
- 业务逻辑正确性
- 性能问题
- 安全问题
- 测试覆盖率

### 4.2 Review 流程
1. 提交 Pull Request
2. 指定 Reviewer
3. Reviewer 进行代码审查
4. 提出修改意见
5. 开发者修改代码
6. 重新审查直到通过

## 5. 版本管理

### 5.1 版本号规范
- 遵循 Semantic Versioning 2.0.0
- 格式：`Major.Minor.Patch`
  - Major: 不兼容的 API 修改
  - Minor: 向下兼容的功能性新增
  - Patch: 向下兼容的问题修复

### 5.2 Tag 管理
- 每次发布打 tag
- tag 格式：`v版本号`，如 `v1.0.0`
- tag 信息包含版本改动说明

## 6. CI/CD 集成

### 6.1 提交检查
- ESLint 检查
- TypeScript 类型检查
- 单元测试
- 提交信息格式检查

### 6.2 自动化部署
- 开发环境：push 到 develop 分支自动部署
- 测试环境：push 到 release 分支自动部署
- 生产环境：push 到 main 分支自动部署 