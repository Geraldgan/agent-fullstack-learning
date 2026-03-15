# Java 后端速查手册（适合快速回捞）

> 目标：帮你把大学学过但长期没实战的 Java / Spring Boot / MySQL / JWT 迅速捡回来，并能直接用于 Agent 项目后端开发。

---

# 一、后端在整个系统里负责什么

前端负责页面和交互，后端负责：
- 接收请求
- 执行业务逻辑
- 查数据库
- 校验权限
- 返回结果
- 接大模型 / 接工具 / 接缓存

在 Agent 项目里，后端通常是核心中枢。

---

# 二、Java 基础速查

## 1. 类和对象
```java
public class User {
    private Long id;
    private String username;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }
}
```

你要重新建立认知：
后端项目里到处都是对象：
- Entity
- DTO
- VO
- Service

## 2. 集合

### List
```java
List<String> list = new ArrayList<>();
list.add("Tom");
```

### Map
```java
Map<String, Object> map = new HashMap<>();
map.put("name", "Tom");
```

### 常见场景
- List：消息列表、会话列表
- Map：临时组织数据

## 3. 泛型
```java
List<User> users = new ArrayList<>();
```

表示列表里的元素类型是 User。

## 4. 异常
```java
try {
    int x = 1 / 0;
} catch (Exception e) {
    e.printStackTrace();
}
```

后端里更常见的是：
- 抛业务异常
- 全局统一捕获

## 5. Stream
```java
List<String> result = names.stream()
        .filter(item -> item.length() > 1)
        .collect(Collectors.toList());
```

你当前目标：能看懂，能写简单过滤和映射。

---

# 三、Spring Boot 速查

## 1. 最常见注解

### 启动类
```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

### Controller
```java
@RestController
@RequestMapping("/api/user")
public class UserController {
}
```

### Service
```java
@Service
public class UserService {
}
```

### 配置类
```java
@Configuration
public class WebConfig {
}
```

## 2. 常用请求注解

### GET
```java
@GetMapping("/list")
public String list() {
    return "ok";
}
```

### POST
```java
@PostMapping("/login")
public String login() {
    return "ok";
}
```

### PathVariable
```java
@GetMapping("/{id}")
public String getById(@PathVariable Long id) {
    return "id=" + id;
}
```

### RequestBody
```java
@PostMapping("/login")
public String login(@RequestBody LoginRequest request) {
    return request.getUsername();
}
```

---

# 四、三层结构速查

## 1. Controller
职责：
- 接收请求
- 调 Service
- 返回结果

## 2. Service
职责：
- 写业务逻辑
- 组合多个操作

## 3. Mapper / Repository
职责：
- 和数据库交互

## 一句话理解
- Controller：门口接待
- Service：真正办事的人
- Mapper：查档案的人

---

# 五、统一响应结构速查

建议统一返回：

```java
public class Result<T> {
    private Integer code;
    private String message;
    private T data;
}
```

常用写法：
```java
public static <T> Result<T> success(T data) {
    Result<T> r = new Result<>();
    r.setCode(0);
    r.setMessage("success");
    r.setData(data);
    return r;
}
```

为什么要统一：
- 前端更容易处理
- 错误和成功结构一致

---

# 六、DTO / Entity / VO 速查

## Entity
数据库实体。

## DTO
接收前端请求参数。

## VO
返回给前端的数据对象。

### 例子
- `LoginRequestDTO`
- `UserEntity`
- `UserInfoVO`

### 为什么不要混着用
因为职责不同，后期维护会更清楚。

---

# 七、MySQL 速查

## 1. 常见 SQL

### 查询
```sql
select * from user;
```

### 条件查询
```sql
select * from conversation where user_id = 1;
```

### 插入
```sql
insert into user(username, password_hash) values('tom', 'xxx');
```

### 更新
```sql
update conversation set title = '新标题' where id = 1;
```

### 删除
```sql
delete from message where id = 1;
```

## 2. 表设计最小模板

### user
- id
- username
- password_hash
- created_at

### conversation
- id
- user_id
- title
- created_at

### message
- id
- conversation_id
- role
- content
- created_at

## 3. 常见关系
- 用户 1 对多 会话
- 会话 1 对多 消息

## 4. 索引先记住什么
高频查询字段考虑建索引：
- user_id
- conversation_id

---

# 八、MyBatis-Plus 速查

## 1. 常见组成
- Entity
- Mapper
- Service

## 2. 最小 Mapper
```java
@Mapper
public interface UserMapper extends BaseMapper<UserEntity> {
}
```

## 3. 常用 CRUD
```java
userMapper.insert(user);
userMapper.selectById(id);
userMapper.updateById(user);
userMapper.deleteById(id);
```

## 4. 条件查询
```java
LambdaQueryWrapper<UserEntity> wrapper = new LambdaQueryWrapper<>();
wrapper.eq(UserEntity::getUsername, username);
UserEntity user = userMapper.selectOne(wrapper);
```

---

# 九、JWT 鉴权速查

## 1. 登录流程
1. 用户输入用户名密码
2. 后端校验
3. 生成 token
4. 前端保存 token
5. 后续请求带 token
6. 后端解析 token

## 2. 前端如何带 token
```http
Authorization: Bearer xxxxxx
```

## 3. 后端要做什么
- 登录接口签发 token
- 拦截请求
- 解析 token 获取 userId

## 4. 你现阶段至少做到
- 用户只能查自己的会话和消息

---

# 十、Redis 速查

## 1. Redis 是什么
高性能内存数据库。

## 2. 常见用途
- 缓存热点数据
- token 辅助存储
- 验证码
- 任务状态

## 3. 现阶段够用认知
- 它比 MySQL 快
- 适合临时、高频数据
- 不适合替代所有持久化数据

---

# 十一、全局异常处理速查

## 为什么要做
不然报错时接口返回结构会乱。

## 典型思路
- 自定义业务异常
- 全局捕获异常
- 返回统一错误结构

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public Result<String> handle(Exception e) {
        return Result.fail("系统异常");
    }
}
```

---

# 十二、日志速查

## 为什么要打日志
出了问题时靠日志排查。

## 该记什么
- 用户关键操作
- 重要参数
- 模型调用过程
- 工具调用失败
- 异常堆栈

## 原则
- 别什么都不打
- 也别把敏感信息全打出来

---

# 十三、文件上传速查

## 为什么重要
RAG 一定会用到文档上传。

## 后端接收文件
```java
@PostMapping("/upload")
public Result<String> upload(@RequestParam("file") MultipartFile file) {
    return Result.success(file.getOriginalFilename());
}
```

## 前端通常怎么传
`multipart/form-data`

---

# 十四、聊天接口最小示例速查

## 请求 DTO
```java
public class ChatRequest {
    private Long conversationId;
    private String content;
}
```

## Controller
```java
@PostMapping("/send")
public Result<String> send(@RequestBody ChatRequest request) {
    return Result.success("模型回复");
}
```

## 你后面真实会做的事情
- 先保存用户消息
- 再调模型
- 再保存模型回复
- 再返回前端

---

# 十五、Agent 项目后端比普通 CRUD 多什么

普通后台系统：
- 增删改查
- 用户权限

Agent 后端多了：
- 模型调用
- Prompt 组装
- Tool Calling 执行器
- RAG 检索
- 长任务与异步流程

所以你学后端时，要把这部分预留在脑子里。

---

# 十六、后端常见报错速查

## 1. 400 Bad Request
参数格式不对，或者少字段。

## 2. 401 Unauthorized
没带 token，或 token 无效。

## 3. 403 Forbidden
有身份，但没权限。

## 4. 500 Internal Server Error
后端代码报错。

排查顺序：
1. 看请求参数
2. 看后端日志
3. 看数据库
4. 看返回结构

---

# 十七、你当前阶段最该达到什么程度

只要你现在能做到这些，就算后端回捞成功：

- 能写 Spring Boot 基础接口
- 能写用户 / 会话 / 消息 CRUD
- 能设计聊天系统表结构
- 能接 MySQL
- 能实现 JWT 登录
- 能处理基本异常
- 能看懂和写简单 MyBatis-Plus 查询

---

# 十八、给你的实用建议

你从 iOS 转 Java 后端，最容易卡在两件事：

## 1. 注解太多
先别背全，只抓最常用那几个。

## 2. 概念多但串不起来
解决方式：始终围绕一个聊天项目去理解。

比如：
- 登录为什么需要 JWT
- 会话为什么要有 user_id
- 消息为什么要有 conversation_id
- 为什么要统一返回结构

一旦围绕真实项目去学，Java 后端会清晰很多。
