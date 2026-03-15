# 一周速成版 Agent 全栈知识手册

> 适合场景：你希望在 7 天内，快速建立 Agent 全栈工程师所需的“最小可用知识闭环”。  
> 目标：不是 7 天变专家，而是 7 天内把必须知道、必须会用、必须能讲的核心知识全部串起来。

---

# 一、这 7 天你到底要学到什么

7 天之后，你至少要做到：

- 知道前端页面怎么搭
- 知道后端接口怎么写
- 知道数据库怎么存聊天数据
- 知道大模型怎么接入
- 知道 Tool Calling 是怎么跑的
- 知道 RAG 的完整流程
- 知道项目怎么部署

换句话说：

**你要建立的是全局地图 + 最小动手能力。**

---

# 二、学习方法：每一天都按这个节奏走

每天分 4 步：

## 第一步：先理解概念
问自己：它是什么？解决什么问题？

## 第二步：记住最核心的 20%
不要一口吃掉全部细节。

## 第三步：写最小 demo
哪怕只有 30 行代码，也必须动手。

## 第四步：把它放回 Agent 项目场景里
想清楚它在你的 Agent 平台里到底用在哪。

---

# Day 1：前端基础——网页、布局、交互到底怎么回事

## 今天目标
搞清楚 Web 前端最基本的构成：
- HTML 负责结构
- CSS 负责样式
- JavaScript 负责交互

---

## 1. HTML 是什么
HTML 就是网页骨架。

你先记住这些标签就够：
- `div`：最常用容器
- `span`：行内容器
- `input`：输入框
- `button`：按钮
- `textarea`：多行输入
- `img`：图片
- `ul/li`：列表
- `form`：表单

### 在 Agent 项目里怎么用
- 左侧会话栏：列表
- 中间消息区：多个消息块
- 底部输入框：input / textarea + button

---

## 2. CSS 是什么
CSS 决定页面长什么样。

### 必学核心
#### 盒模型
元素由：
- 内容 content
- 内边距 padding
- 边框 border
- 外边距 margin
构成。

#### Flex 布局
这是最重要的布局方式。

你先理解 4 个属性：
- `display: flex`
- `flex-direction`
- `justify-content`
- `align-items`

### 在 Agent 项目里怎么用
- 整个页面左右布局
- 输入框和发送按钮横向排
- 消息列表纵向排列

---

## 3. JavaScript 是什么
它让页面“动起来”。

### 你必须掌握
- 变量
- 函数
- 对象
- 数组
- if / for
- map / filter
- Promise
- async / await

### 重点理解：异步
前端调用后端接口不是立刻返回，需要等待。
这就需要：
- Promise
- async / await

### 最小例子
```js
async function loadData() {
  const res = await fetch('/api/demo')
  const data = await res.json()
  console.log(data)
}
```

### 今天必须会的事情
- 能写一个按钮点击事件
- 能写一个输入框取值
- 能写一个异步请求函数

---

## Day 1 最小知识清单
- HTML 结构
- CSS 盒模型
- Flex 布局
- JS 基本语法
- Promise / async await

## Day 1 练习
1. 写一个登录页 HTML
2. 用 CSS 做一个左右布局页面
3. 写一个按钮点击后打印输入框内容

---

# Day 2：React——现代前端怎么组织页面

## 今天目标
理解为什么前端不用原生 JS 堆页面，而要用 React。

---

## 1. React 解决什么问题
React 让页面可以组件化、状态化、可维护。

你可以把它理解成：
- 页面 = 组件树
- 组件 = 可复用 UI 单元
- 状态 = 驱动页面变化的数据

---

## 2. 组件
例如：
- 会话列表组件
- 消息组件
- 输入框组件
- 顶部栏组件

### 组件的核心概念
- props：外部传入的数据
- state：组件内部变化的数据

---

## 3. useState
最重要的 Hook。

### 它解决什么问题
让页面的数据变了，界面自动更新。

### 典型用法
- 保存输入框内容
- 保存消息列表
- 保存 loading 状态

---

## 4. useEffect
### 它解决什么问题
在组件加载后做副作用操作，比如请求接口。

### 常见场景
- 页面打开时拉取会话列表
- 当前会话变化时拉取消息

---

## 5. 列表渲染和条件渲染
### 列表渲染
会话列表、消息列表都要用。

### 条件渲染
比如：
- 有数据才显示
- 没数据显示空状态
- 加载中显示 loading

---

## Day 2 最小知识清单
- 组件
- props / state
- useState
- useEffect
- 条件渲染
- 列表渲染

## Day 2 练习
1. 写一个消息列表组件
2. 写一个输入框组件
3. 把两者组装成聊天页

---

# Day 3：Next.js + TypeScript——做一个真正的前端项目壳子

## 今天目标
知道现代前端项目怎么搭起来，并用 TypeScript 把结构写清楚。

---

## 1. 为什么用 Next.js
因为它比裸 React 更适合做产品项目：
- 目录结构清晰
- 路由方便
- 工程能力强

### 你今天先记住
- page 是页面
- layout 是公共布局
- 目录决定路由

---

## 2. TypeScript 为什么重要
它给 JS 加上类型，让大型项目更稳定。

### 今天必须掌握
- 基本类型
- interface
- type
- 数组类型
- 对象类型
- 联合类型

### 在 Agent 项目里怎么用
例如定义消息：
```ts
type Role = 'user' | 'assistant'

interface Message {
  id: string
  role: Role
  content: string
}
```

---

## 3. 前端项目该怎么拆
建议先这样：
- `app/` 页面
- `components/` 组件
- `services/` 请求
- `types/` 类型
- `hooks/` 逻辑复用

---

## Day 3 最小知识清单
- Next.js 路由概念
- TypeScript 类型系统基础
- 前端目录结构设计
- 接口请求封装基础

## Day 3 练习
1. 搭一个 Next.js 项目
2. 做登录页和聊天页两个页面
3. 写 Message、Conversation 类型定义

---

# Day 4：Java + Spring Boot——后端接口到底怎么写

## 今天目标
理解 Java Web 后端是怎么接住前端请求的。

---

## 1. Java 基础回顾
你重点回忆：
- 类和对象
- List / Map
- 泛型
- 异常
- 注解

不需要重新学整本 Java。

---

## 2. Spring Boot 解决什么问题
它让你快速搭建 Web 服务。

### 你要记住 3 层结构
- Controller：处理请求
- Service：业务逻辑
- Mapper/Repository：访问数据库

---

## 3. 常用注解
先记这些：
- `@RestController`
- `@GetMapping`
- `@PostMapping`
- `@Service`
- `@RequestBody`
- `@PathVariable`

---

## 4. 接口是怎么工作的
例如：
- 前端发 POST `/api/chat/send`
- Controller 接收参数
- Service 处理逻辑
- 返回统一结果

### 统一响应结构为什么重要
建议统一：
- `code`
- `message`
- `data`

---

## Day 4 最小知识清单
- Java 基础回顾
- Spring Boot 三层结构
- Controller / Service 分工
- RequestBody / PathVariable
- 统一响应结构

## Day 4 练习
1. 写一个登录接口
2. 写一个获取会话列表接口
3. 写一个发送消息接口（先 mock 返回）

---

# Day 5：MySQL + JWT——数据存哪、登录怎么做

## 今天目标
知道后端不是只返回字符串，而是要有数据库和用户系统。

---

## 1. MySQL 要掌握什么
### 基础 SQL
- `select`
- `insert`
- `update`
- `delete`
- `where`
- `order by`

### 业务表设计
聊天项目至少要有：
- 用户表
- 会话表
- 消息表

### 为什么这样设计
- 一个用户有多个会话
- 一个会话有多条消息

---

## 2. JWT 登录
### 流程
1. 用户登录
2. 后端校验账号密码
3. 生成 token
4. 前端保存 token
5. 后续请求带 token
6. 后端识别用户身份

### 为什么重要
因为你要做“每个用户只看自己的聊天记录”。

---

## 3. Redis 今天先知道什么
- 它是内存数据库
- 比 MySQL 快
- 常用来做缓存和 session/token 辅助存储

先知道场景，不要求今天就写很多。

---

## Day 5 最小知识清单
- MySQL CRUD
- 用户 / 会话 / 消息表关系
- JWT 登录流程
- Redis 的常见用途

## Day 5 练习
1. 设计 3 张表
2. 写登录接口返回 token
3. 写查询当前用户会话列表接口

---

# Day 6：LLM + Tool Calling——让系统从 CRUD 变成 Agent

## 今天目标
理解 Agent 最关键的部分：模型不是只是“回答”，还会“调用工具”。

---

## 1. LLM 基础
### 你必须知道
- token：模型处理文本的单位
- context window：一次能看的上下文长度
- temperature：输出随机性
- system prompt：系统角色设定

### 你必须理解
大模型会幻觉，所以不能只靠它猜。

---

## 2. Prompt 基础
你写 prompt 时要做到：
- 任务明确
- 输出明确
- 边界明确

例如：
- 不知道就说不知道
- 必须按 JSON 输出
- 必须引用资料来源

---

## 3. Tool Calling 是什么
模型发现自己需要查天气，就不直接瞎答，而是：
1. 告诉系统要调用天气工具
2. 系统执行工具
3. 把结果给模型
4. 模型生成最终回答

### 这是 Agent 和普通 ChatBot 的核心区别之一。

---

## 4. 你今天必须理解的闭环
用户问：北京今天天气怎么样？

流程：
1. 前端发消息给后端
2. 后端把消息送给模型
3. 模型选择 `getWeather(city="北京")`
4. 后端执行天气工具
5. 后端把工具结果再发给模型
6. 模型返回自然语言答案
7. 后端保存消息并返回前端

---

## Day 6 最小知识清单
- token / temperature / system prompt
- Prompt 约束
- Tool Calling 闭环
- 工具 schema 和执行器的概念

## Day 6 练习
1. 设计一个天气工具 schema
2. 设计一个搜索工具 schema
3. 画出工具调用时序图

---

# Day 7：RAG + Workflow + 部署——补完整个闭环

## 今天目标
把 Agent 应用最关键的剩余部分串起来。

---

## 1. RAG 是什么
不是让模型“凭记忆答”，而是：
- 先查资料
- 再基于资料回答

### 核心流程
1. 上传文档
2. 文本切片
3. embedding
4. 向量检索
5. 拼接上下文
6. 模型回答
7. 引用来源

### 为什么必须学
因为企业级 Agent 很多核心价值都来自“接企业私有知识”。

---

## 2. Workflow 是什么
不是一次对话，而是多步执行。

例如研究助手：
1. 搜索资料
2. 提炼重点
3. 生成总结
4. 输出报告

### 你先掌握
- 任务拆解
- 状态流转
- 多步执行

---

## 3. 部署为什么重要
如果你的项目只能本地跑，价值会打折。

### 你至少要知道
- Docker：把环境打包
- Docker Compose：多个服务一起起
- Nginx：做代理入口
- Linux：看日志、查进程

---

## Day 7 最小知识清单
- RAG 全流程
- Workflow 基础思路
- Docker / Compose / Nginx 的角色
- 线上项目的基本组成

## Day 7 练习
1. 画出 RAG 流程图
2. 画出研究助手的多步流程图
3. 写出你的项目部署架构图

---

# 三、这一周结束后，你应该真正掌握的核心知识

如果把 7 天内容再压缩成最终必背版，就是下面这些。

## 前端
- HTML / CSS / JS 基础
- Flex 布局
- React 组件、state、effect
- Next.js 项目结构
- TypeScript 类型定义

## 后端
- Java 基础回顾
- Spring Boot 三层结构
- REST API
- MySQL 表设计与 CRUD
- JWT 登录
- Redis 使用场景

## Agent
- LLM 基础概念
- Prompt 约束
- Tool Calling 闭环
- RAG 全流程
- Workflow 多步任务

## 工程化
- Git
- Linux 基础
- Docker
- Nginx
- 日志排障思路

---

# 四、真正“教会你”的理解方式：把所有知识放回一个项目里

假设你做一个 Agent Chat Platform：

## 用户登录
你要用到：
- 前端表单
- React 状态管理
- Spring Boot 登录接口
- MySQL 用户表
- JWT token

## 用户发消息
你要用到：
- 输入框组件
- 消息列表渲染
- `/api/chat/send` 接口
- MySQL 消息表
- 模型 API 调用

## 模型调用工具
你要用到：
- prompt 设计
- tool schema
- 工具执行器
- 日志记录

## 文档问答
你要用到：
- 文件上传
- 文档切片
- embedding
- 检索
- 引用来源

## 部署上线
你要用到：
- Dockerfile
- Compose
- Nginx
- Linux 命令

只要你能把这些关系串起来，说明你真的开始入门了。

---

# 五、7 天之后怎么接长期 3 个月计划

一周速成的作用是：
- 让你不再迷茫
- 快速知道全局地图
- 知道每块知识为什么存在

接下来你再进入 3 个月计划，就会更顺：
- 第 1 个月：前端 + 后端基础
- 第 2 个月：AI Chat + Tool Calling
- 第 3 个月：RAG + Workflow + 部署

---

# 六、最后给你的建议

如果你问“7 天最该记住什么”，我给你的答案是：

1. 前端是页面和交互
2. 后端是接口和业务
3. 数据库是持久化
4. 大模型是智能能力
5. Tool Calling 是 Agent 行动力
6. RAG 是私有知识能力
7. 部署是产品真正落地

只要你把这 7 件事串起来，你就不是在“零散学技术”，而是在搭建一个完整的 Agent 工程认知体系。

如果你愿意，下一步我还能继续给你本地生成两份更细的速查文档：

1. `前端速查手册（适合iOS转前端）.md`
2. `Java后端速查手册（适合快速回捞）.md`

这两份会更偏“拿来就看、马上能用”的风格。