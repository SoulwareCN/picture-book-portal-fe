# API 接口规范

## 1. 接口设计规范

### 1.1 URL 规范
- 使用 RESTful 风格
- 使用小写字母，单词间用连字符 `-` 分隔
- 使用名词复数形式
- 版本号放在 URL 中

```
# 好的例子
GET /api/v1/users
GET /api/v1/users/123
POST /api/v1/articles

# 不好的例子
GET /api/v1/getUser
GET /api/v1/user/123
POST /api/v1/createArticle
```

### 1.2 HTTP 方法
- GET：获取资源
- POST：创建资源
- PUT：更新资源（全量更新）
- PATCH：更新资源（部分更新）
- DELETE：删除资源

### 1.3 状态码使用
- 200：成功
- 201：创建成功
- 204：删除成功
- 400：请求参数错误
- 401：未认证
- 403：无权限
- 404：资源不存在
- 500：服务器错误

## 2. 请求规范

### 2.1 请求参数
```typescript
// 查询参数
interface QueryParams {
  page?: number;
  pageSize?: number;
  sortBy?: string;
  sortOrder?: 'asc' | 'desc';
  keyword?: string;
}

// 请求体
interface RequestBody {
  // 必填字段使用 required
  required: string;
  // 可选字段使用 ?
  optional?: string;
}
```

### 2.2 请求头
```typescript
{
  'Content-Type': 'application/json',
  'Authorization': 'Bearer ${token}',
  'Accept-Language': 'zh-CN'
}
```

## 3. 响应规范

### 3.1 响应格式
```typescript
interface ApiResponse<T> {
  code: number;        // 业务状态码
  message: string;     // 状态描述
  data: T;            // 响应数据
  timestamp: number;   // 响应时间戳
}
```

### 3.2 成功响应示例
```json
{
  "code": 0,
  "message": "success",
  "data": {
    "id": 1,
    "name": "张三"
  },
  "timestamp": 1677123456789
}
```

### 3.3 错误响应示例
```json
{
  "code": 1001,
  "message": "用户名或密码错误",
  "data": null,
  "timestamp": 1677123456789
}
```

## 4. 错误处理

### 4.1 错误码规范
```typescript
enum ErrorCode {
  SUCCESS = 0,
  PARAM_ERROR = 1000,
  AUTH_ERROR = 1001,
  FORBIDDEN = 1002,
  NOT_FOUND = 1003,
  SYSTEM_ERROR = 2000
}
```

### 4.2 错误信息规范
- 使用统一的错误信息格式
- 提供清晰的错误描述
- 包含错误的具体原因

## 5. 安全规范

### 5.1 认证
- 使用 JWT Token
- Token 在请求头中传递
- 敏感接口使用 HTTPS

### 5.2 权限
- 基于角色的权限控制
- 接口级别的权限控制
- 数据级别的权限控制

## 6. 性能规范

### 6.1 分页
- 默认分页大小：20
- 最大分页大小：100
- 分页参数：page（页码）、pageSize（每页大小）

### 6.2 缓存
- 使用 ETag
- 合理设置 Cache-Control
- 使用 Redis 缓存热点数据

## 7. 版本控制

### 7.1 版本号规范
- 在 URL 中使用版本号
- 主版本号用于不兼容的 API 修改
- 次版本号用于向下兼容的功能性新增

### 7.2 版本升级
- 提供版本升级说明
- 保持向下兼容
- 提供合理的过渡期

## 8. 文档规范

### 8.1 接口文档
- 使用 Swagger/OpenAPI 规范
- 详细的接口说明
- 请求/响应示例
- 错误码说明

### 8.2 文档示例
```yaml
paths:
  /api/v1/users:
    get:
      summary: 获取用户列表
      parameters:
        - name: page
          in: query
          description: 页码
          required: false
          schema:
            type: integer
            default: 1
      responses:
        '200':
          description: 成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserListResponse'
```

## 9. 测试规范

### 9.1 单元测试
- 覆盖主要业务逻辑
- 测试异常情况
- 测试边界条件

### 9.2 接口测试
- 使用 Postman 或类似工具
- 测试各种请求方法
- 测试错误处理
- 测试性能和并发 