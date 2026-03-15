# Java 与前端一周速成教学版

> 目标：不是给你排计划，而是用 7 天时间，把你从 iOS 工程师转向 Web + Java 后端时最需要的知识，按“是什么 → 为什么 → 怎么用 → 示例 → 常见坑”的方式讲清楚。  
> 适合你当前状态：大学学过 Java，但久没用；前端知道得不系统；想尽快建立可实战的认知闭环。

---

# 一、先建立一个总认知：你到底在学什么

你现在不是在分别学“前端”和“后端”，而是在学一个完整系统是怎么工作的。

假设你做一个 Agent Chat 项目：

1. 用户打开网页
2. 前端把页面渲染出来
3. 用户输入一句话
4. 前端把这句话发给后端
5. 后端做业务处理
6. 后端查数据库 / 调大模型 / 调工具
7. 后端把结果返回给前端
8. 前端把结果展示出来

所以：

- **前端**：负责页面、交互、展示
- **后端**：负责业务、数据、权限、接口
- **数据库**：负责存储
- **HTTP**：负责前后端通信

你要学的所有知识，都是围绕这条链路展开。

---

# Day 1：前端最基础的本质 —— HTML / CSS / JS

## 1. HTML 是什么

HTML 就是页面结构。你可以把它理解成 iOS 里 View 层的“骨架”。

比如一个聊天输入区，本质就是：

```html
<div>
  <input placeholder="请输入消息" />
  <button>发送</button>
</div>
```

### 你必须掌握的 HTML 标签

#### 容器类
- `div`：最常用的大盒子
- `span`：小块文本容器

#### 文本类
- `h1 ~ h6`
- `p`

#### 表单类
- `input`
- `textarea`
- `button`
- `form`
- `label`

#### 列表类
- `ul`
- `li`

### 在实战里怎么理解

一个聊天页通常会长这样：

```html
<div class="page">
  <div class="sidebar">会话列表</div>
  <div class="main">
    <div class="messages">消息区域</div>
    <div class="input-area">
      <input />
      <button>发送</button>
    </div>
  </div>
</div>
```

你不用背很多标签，先把这几个用熟就够 80% 项目了。

---

## 2. CSS 是什么

CSS 决定网页“长什么样”。

如果你把 HTML 理解为 UIView 的层级结构，那 CSS 就像：
- frame / layout
- backgroundColor
- font
- margin / padding
- 圆角、边框、阴影

### 2.1 盒模型

每个元素都可以想成一个盒子：

- content：内容
- padding：内边距
- border：边框
- margin：外边距

例如：

```css
.box {
  width: 200px;
  padding: 12px;
  border: 1px solid #ddd;
  margin: 16px;
}
```

### 2.2 Flex 布局

这是你最最最需要掌握的 CSS 知识点。

因为现代后台页面、聊天页面，大量靠 Flex。

```css
.container {
  display: flex;
}
```

#### 最重要的几个属性
- `flex-direction: row | column`
- `justify-content`
- `align-items`
- `gap`
- `flex: 1`

### 例子：左右布局

```css
.page {
  display: flex;
  height: 100vh;
}

.sidebar {
  width: 260px;
  border-right: 1px solid #eee;
}

.main {
  flex: 1;
}
```

### 例子：输入框和按钮并排

```css
.input-area {
  display: flex;
  gap: 8px;
}

.input-area input {
  flex: 1;
}
```

### 你今天一定要真正理解
- 页面不是“写出来就能好看”
- 本质是一个个盒子排列
- Flex 是 Web 页面布局的主力

---

## 3. JavaScript 是什么

JavaScript 是前端逻辑层。你可以理解为：
- 接用户输入
- 改页面状态
- 调接口
- 处理返回结果

### 3.1 基本语法

#### 变量
```js
let name = 'Gerald'
const age = 18
```

#### 函数
```js
function add(a, b) {
  return a + b
}

const add2 = (a, b) => a + b
```

#### 对象
```js
const user = {
  id: 1,
  name: 'Tom'
}
```

#### 数组
```js
const list = [1, 2, 3]
```

### 3.2 数组方法

#### map
把数组转换成另一个数组。

```js
const nums = [1, 2, 3]
const result = nums.map(item => item * 2)
// [2,4,6]
```

#### filter
过滤。

```js
const nums = [1, 2, 3, 4]
const result = nums.filter(item => item > 2)
// [3,4]
```

#### find
找一个。

```js
const users = [{id:1}, {id:2}]
const user = users.find(item => item.id === 2)
```

这几个你在 React 里天天会用到。

### 3.3 异步

前端最关键的认知之一：
**调接口不是同步返回的。**

所以你要会：
- Promise
- async / await

```js
async function fetchData() {
  const res = await fetch('/api/user')
  const data = await res.json()
  console.log(data)
}
```

### 3.4 常见坑

#### `=` / `==` / `===`
优先用 `===`

#### null / undefined
要知道它们不是一回事

#### 直接改对象
React 里不要直接改原对象，要新建一个对象再 setState

---

# Day 2：React —— 前端真正开始像工程了

## 1. React 是什么

React 是一个用来构建 UI 的库。

如果你写原生 HTML + JS，页面复杂起来会很乱。React 帮你把页面拆成组件。

你可以把它类比为：
- iOS 里一个页面由多个 UIView / UIViewController 组成
- React 里一个页面由多个组件组成

---

## 2. 组件

比如聊天页面，你可以拆成：
- `Sidebar`
- `ConversationItem`
- `ChatWindow`
- `MessageBubble`
- `ChatInput`

### 一个最简单的组件

```jsx
function Hello() {
  return <div>Hello React</div>
}
```

---

## 3. props

props 就是组件的输入参数。

```jsx
function MessageBubble(props) {
  return <div>{props.content}</div>
}
```

更常见写法：

```jsx
function MessageBubble({ content }) {
  return <div>{content}</div>
}
```

### 你要理解
- props 像函数参数
- 父组件传给子组件
- 子组件不要乱改 props

---

## 4. state

state 是组件内部会变化的数据。

聊天页面里什么是 state？
- 当前输入内容
- 当前会话 ID
- 消息列表
- loading 状态

### useState

```jsx
import { useState } from 'react'

function Counter() {
  const [count, setCount] = useState(0)

  return (
    <div>
      <div>{count}</div>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  )
}
```

### 核心理解
- `count` 是当前值
- `setCount` 用来更新它
- 更新后 React 会重新渲染页面

---

## 5. useEffect

它用来处理“副作用”。

最常见场景：页面加载后请求数据。

```jsx
import { useEffect, useState } from 'react'

function UserList() {
  const [list, setList] = useState([])

  useEffect(() => {
    async function load() {
      const res = await fetch('/api/users')
      const data = await res.json()
      setList(data)
    }

    load()
  }, [])

  return <div>{list.length}</div>
}
```

### 你要理解
- `[]` 表示只在首次渲染执行一次
- 常用来加载初始化数据

---

## 6. 列表渲染

会话列表、消息列表，本质就是把数组渲染成 UI。

```jsx
function MessageList({ messages }) {
  return (
    <div>
      {messages.map(msg => (
        <div key={msg.id}>{msg.content}</div>
      ))}
    </div>
  )
}
```

### `key` 为什么重要
React 要靠 `key` 知道每个元素是谁。

---

## 7. 条件渲染

```jsx
{loading ? <div>加载中...</div> : <div>加载完成</div>}
```

这个在真实项目里太常见了。

---

# Day 3：TypeScript + Next.js —— 让前端进入现代项目模式

## 1. TypeScript 为什么必须学

因为项目一大，纯 JS 很容易出错。

TypeScript 的意义是：
- 给变量加类型
- 给接口数据加类型
- 提前发现错误

### 1.1 基本类型

```ts
let name: string = 'Tom'
let age: number = 18
let isAdmin: boolean = false
```

### 1.2 interface

```ts
interface User {
  id: number
  name: string
}
```

### 1.3 type

```ts
type Role = 'user' | 'assistant'
```

### 1.4 在项目里的典型写法

```ts
interface Message {
  id: string
  role: 'user' | 'assistant'
  content: string
}
```

### 你学 TS 最重要的目标
- 能看懂类型
- 能给接口数据写类型
- 不追求高级类型体操

---

## 2. Next.js 是什么

Next.js 是 React 框架。

你不用先深究它所有能力，只要先会：
- 创建项目
- 建页面
- 配路由
- 调接口

### 常见目录
- `app/`：页面目录
- `components/`：组件
- `services/`：接口请求
- `types/`：类型定义

### 典型页面结构

```text
src/
  app/
    login/
      page.tsx
    chat/
      page.tsx
  components/
  services/
  types/
```

---

## 3. 前端请求封装

你不应该每个页面都手写 fetch 细节。

可以先封成一个简单函数：

```ts
export async function request(url: string, options?: RequestInit) {
  const res = await fetch(url, options)
  if (!res.ok) {
    throw new Error('request failed')
  }
  return res.json()
}
```

### 为什么要封装
- 统一错误处理
- 统一 token 携带
- 统一 base url

---

# Day 4：Java 回捞 —— 把你大学的 Java 重新捡起来

## 1. 类和对象

```java
public class User {
    private Long id;
    private String name;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }
}
```

### 你要重新建立的认知
Java 后端大量围绕“对象”展开：
- 请求对象 DTO
- 数据库实体 Entity
- 返回对象 VO

---

## 2. 集合

### List
有序，可重复。

```java
List<String> names = new ArrayList<>();
names.add("Tom");
```

### Map
键值对。

```java
Map<String, Object> map = new HashMap<>();
map.put("name", "Tom");
```

### 你在后端里会怎么用
- 一个接口返回多个消息：List<Message>
- 一个配置集合：Map<String, Object>

---

## 3. 泛型

```java
List<User> users = new ArrayList<>();
```

意思是：这个列表里装的是 User。

### 你要理解的本质
泛型让编译器提前帮你发现类型错误。

---

## 4. 异常

```java
try {
    int x = 1 / 0;
} catch (Exception e) {
    e.printStackTrace();
}
```

### 实战认知
Java 后端不会让异常满天飞，要统一处理。

---

## 5. Lambda / Stream

```java
List<String> names = Arrays.asList("a", "bb", "ccc");
List<String> result = names.stream()
        .filter(item -> item.length() > 1)
        .collect(Collectors.toList());
```

### 你不需要上来精通
但至少要能读懂。

---

# Day 5：Spring Boot —— 真正开始写后端接口

## 1. Spring Boot 解决什么问题

快速搭 Web 服务。

你可以把它理解为：
- 帮你把 Java 项目快速变成 HTTP 服务
- 提供依赖注入、配置、MVC 等能力

---

## 2. 三层结构

### Controller
接请求。

### Service
写业务逻辑。

### Mapper / Repository
访问数据库。

### 为什么要这样分
为了代码清晰、职责明确。

---

## 3. 最基本接口长什么样

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

### 这段代码什么意思
- `@RestController`：这是个接口控制器
- `@RequestMapping`：公共路径
- `@GetMapping`：处理 GET 请求

---

## 4. 接收参数

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

## 5. 统一响应结构

建议你实际项目统一这样：

```java
public class Result<T> {
    private Integer code;
    private String message;
    private T data;
}
```

### 为什么要统一
前端处理更稳定，不会每个接口格式都不一样。

---

## 6. 依赖注入

```java
@Service
public class UserService {
}
```

```java
@RestController
public class UserController {
    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

### 你要理解
Controller 不用自己 new Service，而是交给 Spring 管理。

---

# Day 6：MySQL + JWT —— 数据与用户系统

## 1. 数据库表怎么理解

假设你做聊天系统。

### 用户表 user
- id
- username
- password_hash
- created_at

### 会话表 conversation
- id
- user_id
- title

### 消息表 message
- id
- conversation_id
- role
- content

### 关系是什么
- 一个用户有多个会话
- 一个会话有多条消息

---

## 2. 基础 SQL

### 查询
```sql
select * from user;
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

### 条件筛选
```sql
select * from message where conversation_id = 10 order by id asc;
```

---

## 3. JWT 登录

### 流程
1. 前端提交账号密码
2. 后端校验
3. 后端生成 token
4. 前端保存 token
5. 后续请求在请求头里带 token
6. 后端解析 token 得到用户身份

### 为什么常见
很适合前后端分离。

### 你要掌握到什么程度
- 知道完整流程
- 会在前端带 token
- 会在后端校验 token

---

## 4. Redis 是什么

Redis 是高性能内存数据库。

### 你现在先记住 3 个用途
- 缓存热点数据
- 存 token / session 辅助信息
- 做任务状态缓存

不用第一周就深入。

---

# Day 7：把前后端真正连起来，并理解 Agent 为什么跟普通项目不同

## 1. 前后端联调的本质

前端不是单独存在，后端也不是单独存在，它们通过 HTTP 连接。

### 一个完整发送消息流程

前端：
```ts
await request('/api/chat/send', {
  method: 'POST',
  body: JSON.stringify({
    conversationId: 1,
    content: '你好'
  })
})
```

后端：
```java
@PostMapping("/send")
public Result<String> send(@RequestBody ChatRequest request) {
    return Result.success("模型回复内容");
}
```

### 你要理解的核心
- 前端负责发请求和展示结果
- 后端负责处理逻辑和返回结果

---

## 2. Agent 项目和普通 CRUD 项目有什么不同

普通管理系统：
- 用户管理
- 数据列表
- 增删改查

Agent 项目：
- 除了 CRUD
- 还要接 LLM
- 还要工具调用
- 还要知识库检索
- 还要多步任务流

所以你不能只学 Java 和前端，还要多一层 Agent 能力。

---

## 3. Tool Calling 是什么

模型不只是回答，还能决定调用工具。

例如：
用户问：“北京今天天气怎么样？”

不是让模型瞎猜，而是：
1. 模型决定调用天气工具
2. 后端执行天气工具
3. 工具返回结果
4. 模型根据结果生成回答

### 这就是 Agent 的“行动能力”。

---

## 4. RAG 是什么

RAG = 检索增强生成。

不是让模型只靠训练时记忆，而是：
1. 先在你的知识库里查资料
2. 再根据资料回答

### 为什么你以后必须学它
因为企业场景大量是“问公司内部资料”。

---

# 二、这一周结束后，你必须真正吃透的知识点

## 前端
- HTML 基本结构
- CSS 盒模型与 Flex
- JS 变量、函数、对象、数组
- async / await
- React 组件、props、state、effect
- TypeScript 类型定义
- Next.js 基本项目结构

## 后端
- Java 类、对象、集合、异常、泛型
- Spring Boot Controller / Service / Mapper
- GET / POST / RequestBody / PathVariable
- 统一响应结构
- MySQL 基础 SQL
- JWT 登录流程

## 项目认知
- 前后端怎么联调
- 聊天系统表怎么设计
- Agent 项目为什么比普通项目多一层 AI 能力

---

# 三、我直接告诉你“学会”的标准是什么

不是你把定义背下来，而是你能做到：

## 前端学会了的标准
- 能独立写一个聊天页
- 能调用一个后端接口
- 能把返回消息展示出来

## Java 后端学会了的标准
- 能独立写一个登录接口
- 能写一个会话列表接口
- 能写一个发送消息接口
- 能接数据库查数据

## 整体学会了的标准
- 能自己讲清楚：用户发一句话后，系统里发生了什么

如果你能讲清这条链路，说明你不是在死记硬背，而是真的懂了。

---

# 四、给你一句最实在的话

你现在最缺的不是“更多资料”，而是：

- 把前端当成页面 + 交互系统去理解
- 把后端当成业务 + 数据系统去理解
- 把 Agent 当成“模型 + 工具 + 知识库”的增强层去理解

只要这个认知一建立，后面的 3 个月系统学习就会顺很多。

如果你愿意，下一步我还可以继续给你补一份：

`Java与前端三个月系统教学版.md`

那份我会按模块深入讲，不是 7 天速成，而是分章节把：
- 前端基础 → React → Next.js → 工程化
- Java 基础 → Spring Boot → MySQL → Redis → 鉴权

全部讲成系统教材式文档。