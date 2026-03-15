# Java 后端系统教学版（从 Java 到 Spring Boot）

> 目标：把你从“大学学过 Java、但没怎么实战”带到“能独立做一个 Agent 项目后端”。  
> 适合对象：有开发经验，想快速系统回捞 Java Web、Spring Boot、MySQL、JWT、Redis 等后端核心知识。

---

# 第一章：后端到底在干什么

很多人学后端时，一上来就被术语淹没：
- Controller
- Service
- Mapper
- JWT
- Redis
- MySQL
- IOC
- AOP

其实你先抓本质就够了。

后端做的事情可以概括为：

1. 接收前端请求
2. 校验参数和权限
3. 执行业务逻辑
4. 读写数据库
5. 返回结果

在 Agent 项目里还会再多几件事：
- 调模型
- 调工具
- 做检索
- 跑异步任务

所以后端本质是一个“业务中枢”。

---

# 第二章：Java 基础回捞——后端世界的基本积木

## 2.1 类和对象

Java 是典型面向对象语言。

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

### 为什么这很重要
因为后端项目里几乎一切都是对象：
- 请求参数对象
- 数据库实体对象
- 返回对象
- 服务对象

---

## 2.2 封装、继承、多态

你不需要现在深挖面试八股，但要有基本认知：
- 封装：把数据和行为包在类里
- 继承：复用父类能力
- 多态：同一接口有不同实现

在业务开发里，最常直接感受到的是“封装”。

---

## 2.3 集合框架

### List
有序，可重复。

```java
List<String> names = new ArrayList<>();
names.add("Tom");
```

### Set
无重复。

### Map
键值对。

```java
Map<String, Object> map = new HashMap<>();
map.put("name", "Tom");
```

### 在项目里怎么用
- 会话列表：`List<Conversation>`
- 参数映射：`Map<String, Object>`

---

## 2.4 泛型

```java
List<User> users = new ArrayList<>();
```

表示这个列表里放的是 User。

### 你要理解的本质
泛型是让编译器替你提前拦住类型错误。

---

## 2.5 异常

### try-catch
```java
try {
    int x = 1 / 0;
} catch (Exception e) {
    e.printStackTrace();
}
```

### 在后端里的真实用法
- 抛业务异常
- 全局统一处理
- 返回稳定错误结构

---

## 2.6 Lambda 和 Stream

```java
List<String> result = names.stream()
        .filter(item -> item.length() > 1)
        .collect(Collectors.toList());
```

### 你现在要达到的程度
- 会读
- 会写简单过滤和映射
- 不追求炫技

---

# 第三章：Spring Boot——让 Java 变成 Web 服务

## 3.1 为什么需要 Spring Boot

如果只有 Java 基础，你只是能写本地程序。Spring Boot 让你快速拥有：
- HTTP 接口
- 配置管理
- 依赖注入
- Web 框架能力

它本质上是 Java Web 开发的高效框架。

---

## 3.2 启动类

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

它是整个项目的入口。

---

## 3.3 Controller

Controller 负责接住 HTTP 请求。

```java
@RestController
@RequestMapping("/api/user")
public class UserController {

    @GetMapping("/hello")
    public String hello() {
        return "hello";
    }
}
```

### 你要理解
- 前端访问某个 URL
- Spring Boot 把它路由到对应方法

---

## 3.4 常见请求注解

### `@GetMapping`
处理 GET 请求。

### `@PostMapping`
处理 POST 请求。

### `@PathVariable`
读取路径参数。

```java
@GetMapping("/{id}")
public String getById(@PathVariable Long id) {
    return "id=" + id;
}
```

### `@RequestBody`
读取请求体 JSON。

```java
@PostMapping("/login")
public String login(@RequestBody LoginRequest request) {
    return request.getUsername();
}
```

---

## 3.5 Service

Service 放业务逻辑。

```java
@Service
public class UserService {
    public String hello() {
        return "hello";
    }
}
```

### 为什么不能都写在 Controller 里
因为接口层和业务层职责不同。代码分层后，维护和扩展都更轻松。

---

## 3.6 依赖注入

```java
@RestController
public class UserController {
    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

### 本质理解
对象由 Spring 管理，而不是你手动 `new`。

这就是 IOC / DI 的核心体验。

---

# 第四章：分层架构——为什么 Java 项目总爱分 Controller / Service / Mapper

## 4.1 标准三层

### Controller
接请求、回响应。

### Service
执行业务逻辑。

### Mapper
负责查数据库。

---

## 4.2 为什么一定要分层

不分层，项目很快会变成一个巨大的“上帝类”。

分层的好处：
- 代码职责清晰
- 更容易测试
- 更容易维护
- 后期功能扩展更稳

---

## 4.3 一个真实链路

用户发送消息：
1. Controller 收到 `/api/chat/send`
2. Service 保存用户消息
3. Mapper 写数据库
4. Service 调模型
5. Service 保存模型回复
6. Controller 返回结果

这就是典型后端链路。

---

# 第五章：统一响应和异常处理——让接口可维护

## 5.1 为什么要统一响应结构

如果每个接口返回格式都不同，前端会很难写。

建议统一：

```java
public class Result<T> {
    private Integer code;
    private String message;
    private T data;
}
```

### 成功返回示例
```java
return Result.success(data);
```

### 失败返回示例
```java
return Result.fail("参数错误");
```

---

## 5.2 全局异常处理

你不应该把每个异常都在 Controller 里 try-catch。

更好的方式是统一捕获。

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public Result<String> handle(Exception e) {
        return Result.fail("系统异常");
    }
}
```

### 为什么重要
这样前端无论遇到什么错误，收到的结构都稳定。

---

# 第六章：MySQL——后端的数据根基

## 6.1 为什么数据库重要

后端没有数据库，大多数业务都没有持久化价值。

对于聊天系统，你至少要保存：
- 用户
- 会话
- 消息

---

## 6.2 基础 SQL

### 查
```sql
select * from user;
```

### 插
```sql
insert into user(username, password_hash) values('tom', 'xxx');
```

### 改
```sql
update conversation set title = '新标题' where id = 1;
```

### 删
```sql
delete from message where id = 1;
```

### 条件和排序
```sql
select * from message where conversation_id = 10 order by id asc;
```

---

## 6.3 表设计思维

一个基础聊天系统可以这样设计：

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

### 关系
- 一个用户有多个会话
- 一个会话有多条消息

---

## 6.4 索引与事务

### 索引
高频查询字段加索引，如：
- user_id
- conversation_id

### 事务
多个操作要么都成功，要么都失败。

例如：
- 新建会话
- 初始化一条系统消息

这两个动作如果必须同时成功，就可能需要事务。

---

# 第七章：MyBatis-Plus——高效访问数据库

## 7.1 为什么学它

因为它能快速完成大量 CRUD。

---

## 7.2 基本组成
- Entity
- Mapper
- Service

### Mapper 示例
```java
@Mapper
public interface UserMapper extends BaseMapper<UserEntity> {
}
```

### 基础 CRUD
```java
userMapper.insert(user);
userMapper.selectById(id);
userMapper.updateById(user);
userMapper.deleteById(id);
```

---

## 7.3 条件查询

```java
LambdaQueryWrapper<UserEntity> wrapper = new LambdaQueryWrapper<>();
wrapper.eq(UserEntity::getUsername, username);
UserEntity user = userMapper.selectOne(wrapper);
```

### 你要理解
业务开发的大部分数据库访问，不一定都要手写 SQL。

---

# 第八章：JWT——前后端分离项目的登录基础

## 8.1 为什么需要 JWT

因为前后端分离后，后端通常不再像老式服务端模板那样天然维护页面 Session 状态。

JWT 可以让前端在每次请求时带上身份信息。

---

## 8.2 登录流程

1. 用户输入账号密码
2. 后端校验
3. 生成 token
4. 前端保存 token
5. 请求头带 token
6. 后端解析 token 得到 userId

---

## 8.3 在项目中的核心目标

不是“实现 JWT”本身，而是：
- 用户只能访问自己的数据
- 未登录不能访问受保护接口

---

# 第九章：Redis——让后端更像真实工程

## 9.1 Redis 的价值

Redis 是高性能内存存储，适合：
- 缓存
- 登录态辅助
- 验证码
- 任务状态

---

## 9.2 你现阶段最该理解的场景

### 缓存热点数据
比如会话列表短时间内频繁访问。

### token / session 辅助信息
比如黑名单、登录态扩展信息。

### 任务状态
比如一个长任务是否完成。

---

# 第十章：文件上传——迈向 RAG 的第一步

## 10.1 为什么重要

因为知识库问答一定离不开文档上传。

## 10.2 Spring Boot 接收文件

```java
@PostMapping("/upload")
public Result<String> upload(@RequestParam("file") MultipartFile file) {
    return Result.success(file.getOriginalFilename());
}
```

### 上传之后常见动作
- 保存文件到本地或对象存储
- 把文件名、路径、用户 id 存数据库
- 后续做解析和切片

---

# 第十一章：日志——出问题时你靠什么活下来

## 11.1 为什么日志特别重要

项目跑起来之后，问题不会只发生在编译期，更多会发生在运行时。

这时你最依赖的是日志。

---

## 11.2 该记录什么

- 用户关键操作
- 请求参数摘要
- 模型调用过程
- 工具调用过程
- 错误堆栈

### 但注意
不要把密码、token、敏感隐私全部打进日志。

---

# 第十二章：面向 Agent 项目的后端思维

这是你和普通 CRUD 后端拉开差距的地方。

## 12.1 Agent 后端多了什么

除了普通业务后端的能力，还多了：
- 模型调用
- Prompt 组装
- Tool Calling
- RAG 检索
- 异步任务与工作流

## 12.2 一个聊天请求的真实流程

1. 前端传来用户消息
2. 后端保存消息
3. 读取上下文历史
4. 组装 prompt
5. 调模型
6. 如果模型要求调用工具，则执行工具
7. 工具结果回给模型
8. 保存模型回复
9. 返回前端

### 这就是 Agent 项目的中枢逻辑。

---

# 第十三章：你应该掌握到什么程度

你读完并练完这份教材后，目标不是变成资深架构师，而是达到：

- 能独立搭一个 Spring Boot 项目
- 能设计用户、会话、消息表
- 能写 CRUD 和聊天接口
- 能做登录鉴权
- 能接 MySQL 和简单 Redis
- 能做文件上传
- 能理解 Agent 后端为什么比普通 CRUD 更复杂

---

# 第十四章：给你的最重要建议

你从 iOS 转 Java 后端时，最容易犯的错是：
- 被术语吓住
- 一开始就陷入底层原理
- 学很多概念却不做项目

最有效的方式是：
- 每学一章，就回到聊天项目里找落点
- 每学一个知识点，都问自己它在系统链路中干什么
- 先能做，再逐步加深原理

你真正的目标不是“会背 Java 八股”，而是：

**能独立写出一个支撑 Agent 产品的后端。**
