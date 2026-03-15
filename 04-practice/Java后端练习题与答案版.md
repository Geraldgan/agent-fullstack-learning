# Java 后端练习题与答案版

> 目标：帮助你把 Java / Spring Boot / MySQL / JWT 真正写出来，而不是停留在“看懂”。

---

# 第一部分：Java 基础练习

## 题目 1：定义一个 User 类

要求：
- id: Long
- username: String
- getter / setter

### 参考答案
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

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }
}
```

---

## 题目 2：创建一个 List 并添加两个用户名

### 参考答案
```java
List<String> names = new ArrayList<>();
names.add("Tom");
names.add("Jerry");
```

---

## 题目 3：用 Stream 过滤长度大于 3 的字符串

### 参考答案
```java
List<String> names = Arrays.asList("Tom", "Jerry", "Alice");
List<String> result = names.stream()
        .filter(item -> item.length() > 3)
        .collect(Collectors.toList());
```

---

# 第二部分：Spring Boot 练习

## 题目 4：写一个 Hello 接口

### 参考答案
```java
@RestController
@RequestMapping("/api/test")
public class TestController {

    @GetMapping("/hello")
    public String hello() {
        return "hello";
    }
}
```

---

## 题目 5：写一个带 PathVariable 的接口

### 参考答案
```java
@GetMapping("/{id}")
public String getById(@PathVariable Long id) {
    return "id=" + id;
}
```

---

## 题目 6：写一个接收 RequestBody 的登录接口

### DTO
```java
public class LoginRequest {
    private String username;
    private String password;

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}
```

### Controller
```java
@PostMapping("/login")
public String login(@RequestBody LoginRequest request) {
    return request.getUsername();
}
```

---

# 第三部分：统一响应练习

## 题目 7：定义一个通用 Result 类

### 参考答案
```java
public class Result<T> {
    private Integer code;
    private String message;
    private T data;

    public static <T> Result<T> success(T data) {
        Result<T> r = new Result<>();
        r.setCode(0);
        r.setMessage("success");
        r.setData(data);
        return r;
    }

    public Integer getCode() {
        return code;
    }

    public void setCode(Integer code) {
        this.code = code;
    }

    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }
}
```

---

# 第四部分：MySQL 练习

## 题目 8：设计用户表

### 参考答案
```sql
create table user (
  id bigint primary key auto_increment,
  username varchar(64) not null,
  password_hash varchar(255) not null,
  created_at datetime default current_timestamp
);
```

---

## 题目 9：设计会话表

### 参考答案
```sql
create table conversation (
  id bigint primary key auto_increment,
  user_id bigint not null,
  title varchar(255) not null,
  created_at datetime default current_timestamp
);
```

---

## 题目 10：查询某个会话下的所有消息

### 参考答案
```sql
select * from message
where conversation_id = 1
order by id asc;
```

---

# 第五部分：MyBatis-Plus 练习

## 题目 11：定义一个 Mapper

### 参考答案
```java
@Mapper
public interface UserMapper extends BaseMapper<UserEntity> {
}
```

---

## 题目 12：按用户名查询用户

### 参考答案
```java
LambdaQueryWrapper<UserEntity> wrapper = new LambdaQueryWrapper<>();
wrapper.eq(UserEntity::getUsername, username);
UserEntity user = userMapper.selectOne(wrapper);
```

---

# 第六部分：JWT 练习

## 题目 13：写出登录流程

### 标准答案
1. 用户提交账号密码
2. 后端校验账号密码
3. 生成 token
4. 返回 token 给前端
5. 前端保存 token
6. 以后每次请求带 token
7. 后端解析 token 获取用户身份

---

# 第七部分：综合实战题

## 题目 14：写一个发送消息接口

要求：
- 接收 conversationId 和 content
- 返回“模型回复”

### DTO
```java
public class ChatRequest {
    private Long conversationId;
    private String content;

    public Long getConversationId() {
        return conversationId;
    }

    public void setConversationId(Long conversationId) {
        this.conversationId = conversationId;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }
}
```

### Controller
```java
@RestController
@RequestMapping("/api/chat")
public class ChatController {

    @PostMapping("/send")
    public Result<String> send(@RequestBody ChatRequest request) {
        return Result.success("模型回复");
    }
}
```

---

# 第八部分：自测标准

如果你能独立写出下面这些，就说明 Java 后端已经开始回捞成功：

- Java 类和集合
- Spring Boot Controller
- RequestBody / PathVariable
- 通用 Result 返回结构
- 基础 SQL
- MyBatis-Plus Mapper 查询
- 一个最小聊天接口

接下来你就能开始做完整项目后端了。
