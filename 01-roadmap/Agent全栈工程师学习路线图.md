# Agent 全栈工程师学习路线图（适合 iOS 开发转型）

> 适合背景：有 iOS 开发经验，会 Objective-C / Swift，学过 Java，但后端实战较少。  
> 目标：从移动端工程师转为能独立完成前端、后端、Agent 应用开发与部署的 Agent 全栈工程师。

---

# 一、转型目标概览

Agent 全栈工程师，核心不是只会调用大模型 API，而是具备完整的产品落地能力：

- 能做前端页面和交互
- 能写后端 API 和业务逻辑
- 能接入数据库、缓存、鉴权、任务系统
- 能接入 LLM、Tool Calling、RAG、Workflow
- 能完成部署上线、日志排查、工程化管理

你目前的基础并不差：

- 有客户端开发经验
- 有工程化意识
- 熟悉编程与调试
- 学过 Java，可快速捡回后端知识

真正要补的是：

- Web 前端生态
- Java 后端实战
- Agent 系统设计与工程落地
- 部署运维基础

---

# 二、速成版知识点（先做出项目）

这个版本的目标是：先能做出作品，尽快形成可演示项目。

## 2.1 前端速成版

### Web 基础
- HTML 常用标签：div、span、input、button、form、table、img
- CSS 基础：盒模型、Flex、Grid、Position、响应式
- JavaScript 基础：
  - 变量、函数、对象、数组
  - map / filter / reduce
  - Promise / async await
  - 模块化 import / export
  - fetch / axios

### TypeScript
重点掌握：
- 基本类型
- interface / type
- 泛型基础
- 联合类型
- 类型推断
- 可选参数

### React
必须掌握：
- JSX
- 组件化开发
- props / state
- useState / useEffect
- 条件渲染
- 列表渲染
- 表单处理
- 自定义 Hook 基础
- 组件通信

### Next.js
建议直接学，用于快速做 Agent Web 产品：
- 项目结构
- App Router
- 页面路由
- API Route
- 服务端 / 客户端组件基本认知
- 环境变量
- 请求接口并展示数据

### UI 方案
推荐：
- Tailwind CSS
- shadcn/ui

原因：上手快，页面效果容易做得像样。

---

## 2.2 后端速成版（Java / Spring Boot）

### Java 回顾
重点回顾：
- 面向对象
- 集合：List / Set / Map
- 泛型
- 异常
- IO 基础
- 多线程基础
- Lambda / Stream
- 注解

### Spring Boot 核心
必须掌握：
- Spring Boot 项目搭建
- Controller / Service / Repository 分层
- 依赖注入
- application.yml 配置
- RESTful API 设计
- 参数校验
- 全局异常处理
- 日志

### MySQL
要掌握：
- CRUD
- where / order by / group by
- join
- 索引基础
- 事务基础
- 表结构设计

### ORM
建议优先学习：
- MyBatis / MyBatis-Plus

重点：
- 实体映射
- CRUD
- 条件查询
- 分页

### Redis
需要掌握：
- 缓存
- token/session 辅助存储
- 计数器
- 过期时间
- 分布式锁概念

### 安全鉴权
至少掌握：
- JWT
- 登录流程
- 权限控制基础
- 密码加密存储
- CORS

### 异步任务
先掌握：
- Spring 异步执行
- `@Scheduled` 定时任务

再进阶：
- RabbitMQ / Kafka

---

## 2.3 Agent 速成版

### LLM 基础
要理解：
- token
- context window
- temperature
- system / user / assistant message
- embeddings
- structured output
- function calling

### Prompt Engineering
掌握：
- 角色设定
- 输出约束
- few-shot
- 任务拆解
- 避免模型胡说的提示方式

### Tool Calling
核心要点：
- 给模型定义工具
- 模型决定调用哪个工具
- 工具执行并返回结果
- 模型结合结果继续回答

### RAG
要理解：
- 文档切片
- embedding
- 向量检索
- 上下文拼接
- 召回与重排基本概念

### Memory
要理解：
- 短期记忆：当前对话上下文
- 长期记忆：用户偏好 / 历史记录
- 外部存储：数据库 / 向量库

### Workflow
要理解：
- 单 Agent
- Router Agent
- Planner-Executor
- 多步任务流
- 人工确认节点

---

## 2.4 工程化速成版

至少掌握：
- Git
- Linux 常用命令
- Docker 基础
- 接口调试（Postman / Apifox）
- 部署一个项目到云服务器
- Nginx 反向代理基础

---

# 三、详细版知识图谱（系统补全）

---

## 3.1 前端详细版

### 第一层：Web 基础
- 浏览器工作原理基础
- HTTP / HTTPS
- DNS 基本概念
- Cookie / Session / LocalStorage / SessionStorage
- 跨域与 CORS

### 第二层：HTML / CSS
- HTML5 常用标签
- 表单与校验
- Flex / Grid
- BFC
- 选择器优先级
- 动画与过渡
- 媒体查询

### 第三层：JavaScript
- 原型链
- this
- 闭包
- 作用域
- 事件循环
- Promise
- async / await
- 防抖 / 节流
- 深拷贝 / 浅拷贝
- DOM / BOM
- 模块化

### 第四层：TypeScript
- 类型系统
- 泛型
- 工具类型
- 类型守卫
- interface vs type
- declaration file 基础

### 第五层：React
- 组件设计
- Hooks 使用与理解
- 状态提升
- Context
- 性能优化
- memo / useMemo / useCallback
- React Query / SWR
- 表单库
- 错误边界

### 第六层：Next.js
- SSR / CSR / SSG / ISR
- App Router
- Route Handlers
- Server Actions 基础
- Middleware
- SEO 基础
- 部署到 Vercel / 自建服务器

### 第七层：前端工程化
- npm / pnpm
- Vite / Webpack 基础认知
- ESLint / Prettier
- 环境变量管理
- 打包部署
- 前端监控基础

---

## 3.2 后端详细版（Java / Spring Boot）

### 第一层：Java 核心
- 面向对象
- 集合框架
- 泛型
- 反射
- 注解
- 异常体系
- IO / NIO
- 并发编程
- JVM 基础
- GC 基本理解

### 第二层：Spring 体系
- IOC / AOP
- Bean 生命周期
- 自动装配
- Spring MVC
- Spring Boot 自动配置
- 配置加载机制

### 第三层：Web API
- RESTful 设计
- 参数校验
- 统一响应结构
- 全局异常处理
- 文件上传下载
- Swagger / OpenAPI

### 第四层：数据层
- MySQL 设计规范
- 索引
- 事务
- 锁
- MyBatis / MyBatis-Plus
- 分页查询
- 动态 SQL

### 第五层：中间件
- Redis
- RabbitMQ / Kafka
- Elasticsearch 基础
- 对象存储基础

### 第六层：安全
- Spring Security 基础
- JWT
- OAuth2 基础认知
- RBAC 权限模型
- 接口限流
- 防刷、防重复提交

### 第七层：分布式与高并发基础
- 缓存一致性
- 分库分表概念
- 负载均衡
- 限流熔断降级
- 幂等性
- 分布式锁

### 第八层：部署运维
- Linux
- Docker
- Docker Compose
- Nginx
- Jenkins / GitHub Actions
- 日志与监控
- JVM 调优基础认知

---

## 3.3 Agent / AI 应用详细版

### 第一层：LLM 基础
- 大模型是什么
- Transformer 基础认知
- token
- embedding
- 推理 vs 训练
- 上下文窗口
- 幻觉问题

### 第二层：Prompt Engineering
- 指令设计
- 输出结构控制
- few-shot
- chain-of-thought 的认知层理解
- ReAct 思路
- 约束式 Prompt

### 第三层：Tool Use
- 工具 schema 设计
- 函数调用协议
- 错误处理
- 重试机制
- 工具权限隔离

### 第四层：RAG
- 文档清洗
- chunking
- embedding 模型
- 向量数据库
- 检索策略
- rerank
- 上下文压缩

### 第五层：Agent Architecture
- 单 Agent
- 多 Agent
- Router
- Planner
- Executor
- Critic / Evaluator
- Memory layer
- Human-in-the-loop

### 第六层：Agent Engineering
- 任务状态管理
- 长任务异步执行
- 工具调用日志
- Trace
- Prompt versioning
- Evaluation
- Cost control
- Fallback model
- Guardrails

### 第七层：生产化
- 用户隔离
- 权限系统
- 配额系统
- 速率限制
- 审计日志
- 可观测性
- AB testing
- 故障恢复

---

# 四、最适合你的学习顺序

基于你的背景，不建议平均用力，建议分阶段推进。

## 阶段 1：先补齐“能做界面 + 能写接口”
学习顺序：
1. JavaScript / TypeScript
2. React
3. Next.js
4. Java 回顾
5. Spring Boot
6. MySQL
7. Redis

## 阶段 2：快速切入 Agent
1. LLM API 调用
2. Prompt
3. Tool Calling
4. RAG
5. Agent Workflow

## 阶段 3：补工程化与部署
1. Docker
2. Linux
3. Nginx
4. 云部署
5. 日志监控
6. 异步任务 / MQ

---

# 五、12 周速成学习路线（手把手版）

目标：12 周做出 2~3 个可展示的 Agent 项目。

## 第 1-2 周：前端入门
学习内容：
- HTML / CSS / JavaScript 基础
- TypeScript 基础
- React 基础

练习：
- 待办列表
- 聊天页面
- 表单页面

产出：
- 登录页
- 聊天输入框
- 消息列表组件

---

## 第 3-4 周：Next.js + 前端工程化
学习内容：
- Next.js 路由
- API 请求
- Tailwind
- 组件拆分
- 状态管理基础

练习：
- 做一个 AI Chat Web 页面
- 左侧会话栏 + 中间聊天区 + 右侧配置栏

产出：
- 一个类似 ChatGPT 的前端壳子

---

## 第 5-6 周：Java + Spring Boot 回归实战
学习内容：
- Spring Boot 项目搭建
- Controller / Service / DAO
- MySQL 接入
- MyBatis-Plus
- JWT 登录

练习：
- 登录注册
- 聊天会话 CRUD
- 消息记录 CRUD

产出：
- 一个能提供 API 的后端服务

---

## 第 7 周：前后端联调
学习内容：
- axios / fetch
- token 携带
- 跨域处理
- 错误码处理

练习：
- 前端登录
- 拉取会话列表
- 发送消息
- 展示历史聊天

产出：
- 完整可用的 Chat 产品雏形

---

## 第 8 周：接入大模型
学习内容：
- 模型 API 调用
- 流式输出
- Prompt 基础
- 对话上下文拼接

练习：
- 前端流式显示回复
- 后端代理调用模型接口
- 保存聊天记录

产出：
- 一个真正可用的 AI Chat 应用

---

## 第 9 周：接入工具调用
学习内容：
- Function Calling
- Tool Schema
- 工具执行器设计

练习：
实现 3 个工具：
- 天气查询
- 网页搜索
- 待办写入

产出：
- 一个会调用工具的 Agent

---

## 第 10 周：做 RAG
学习内容：
- 文档上传
- 分块
- embedding
- 向量检索
- 回答引用来源

练习：
- 上传 PDF / Markdown
- 问答并引用来源片段

产出：
- 一个知识库问答 Agent

---

## 第 11 周：异步任务 + 工作流
学习内容：
- 长任务状态管理
- 定时任务
- 多步 Workflow 基本思想

练习：
做一个“研究助手”：
- 输入主题
- 搜索资料
- 汇总结果
- 生成报告

产出：
- 一个更像 Agent 的任务系统

---

## 第 12 周：部署上线
学习内容：
- Docker
- Nginx
- 云服务器部署
- 日志查看

练习：
- 前后端打包
- 部署到服务器
- 域名访问

产出：
- 可演示项目链接
- GitHub 仓库
- 简历项目素材

---

# 六、建议你做的 3 个核心项目

## 项目 1：Agent Chat Platform
功能：
- 登录注册
- 会话管理
- 聊天
- 流式输出
- 多模型切换
- 工具调用

技术栈：
- 前端：Next.js + React + Tailwind
- 后端：Spring Boot + MySQL + Redis
- AI：OpenAI / Claude API

你会学到：
- 前端页面搭建
- 后端 API 设计
- 鉴权
- 模型接入
- 流式返回

---

## 项目 2：RAG 知识库助手
功能：
- 上传文档
- 文档切片
- 向量检索
- 问答
- 引用来源

技术建议：
- Spring Boot 做业务后端
- embedding / 向量检索可单独做服务
- 向量库可选：pgvector / Milvus / Qdrant

你会学到：
- RAG 全流程
- 文件处理
- 文本切片
- 检索增强生成

---

## 项目 3：Agent 工作流助手
功能：
- 输入任务
- 自动拆解
- 调用搜索工具
- 汇总信息
- 生成报告
- 保存任务执行记录

你会学到：
- Planner-Executor 模式
- 异步任务
- 工作流状态机
- Agent orchestration

---

# 七、学习方法建议：按项目倒推，不按课程堆积

每学一个知识点，问自己三件事：
1. 这个知识点解决什么问题？
2. 在我的 Agent 项目里会用在哪里？
3. 我能不能马上写一个最小 demo？

例如：

## 学 React
不是为了背 Hook 定义，而是为了实现：
- 聊天输入框
- 消息气泡
- 会话列表
- 模型配置面板

## 学 Spring Boot
不是为了背 IOC / AOP，而是为了实现：
- `/login`
- `/chat/send`
- `/conversation/list`
- `/knowledge/search`

## 学 Redis
不是为了背概念，而是为了实现：
- token 缓存
- 会话上下文缓存
- 限流
- 任务状态管理

---

# 八、优先级建议

## P0 必学
- JavaScript / TypeScript
- React
- Next.js
- Java 基础回顾
- Spring Boot
- MySQL
- REST API
- Git
- Docker
- LLM API 调用
- Prompt
- Tool Calling

## P1 重要
- Redis
- JWT
- RAG
- Linux
- Nginx
- 异步任务
- 日志系统

## P2 进阶
- Spring Security
- Kafka / RabbitMQ
- 向量数据库
- 多 Agent 系统
- 评估与监控
- 高并发与分布式

---

# 九、基于你背景的转型建议

## 你的优势
- 工程习惯通常较好
- 熟悉客户端交互与用户体验
- 对网络请求、状态管理、页面逻辑不陌生
- Java 有历史基础，回捞成本低

## 你的短板
- 对前端生态陌生
- 后端工程实战偏少
- Linux / Docker / 部署经验不足
- Agent 系统设计经验少

## 最优策略
不要先花半年纯学理论。  
最优方案是：
- 边补基础
- 边做项目
- 边沉淀作品集

你真正需要形成的不是“知道很多知识点”，而是：
- Web 工程感
- 后端工程感
- Agent 产品落地能力

---

# 十、推荐技术栈（适合速成）

## 前端
- TypeScript
- React
- Next.js
- Tailwind CSS
- shadcn/ui

## 后端
- Java 17+
- Spring Boot
- MyBatis-Plus
- MySQL
- Redis

## Agent / AI
- OpenAI / Claude / Gemini API
- 先自己写简单 Agent Loop
- 再逐步了解 LangChain / LangGraph

## 部署
- Docker
- Nginx
- Ubuntu / Linux

---

# 十一、现阶段不要踩的坑

## 1. 不要一开始深挖过底层
比如：
- React Fiber
- JVM 调优深水区
- 复杂分布式架构
- 特别重的多 Agent 编排框架

这些可以后补，不是当前最值钱的。

## 2. 不要只看教程不动手
Agent 方向最怕：概念懂很多，但做不出产品。

## 3. 不要一开始追求复杂架构
先把单体系统跑通：
- 前端
- 后端
- 数据库
- 模型调用
- 工具调用

跑通后再拆分。

## 4. 不要一开始被框架绑架
建议顺序：
- 先理解 Tool Calling 原理
- 再看 LangChain / LangGraph
- 先自己实现简单 RAG
- 再逐步接更复杂平台

---

# 十二、每日学习模板（每天 2~3 小时）

## 1 小时：学知识点
例如：
- React Hooks
- Spring Boot Controller
- JWT
- RAG Chunking

## 1 小时：写最小 Demo
学完马上写。

## 30 分钟：整理笔记
记录：
- 这个知识点解决什么问题
- 我踩了什么坑
- 它在 Agent 项目里怎么用

## 30 分钟：推进项目
哪怕只完成一个小功能也行。

---

# 十三、面向转岗 / 找工作的简历思路

简历要传达的不是：
“我是一个会调大模型 API 的 iOS 开发。”

而是：
“我是一个能独立完成 Agent 产品前后端开发、模型接入、工具调用、RAG 与部署落地的工程师。”

建议重点描述：
- 独立设计并实现 AI Chat 平台
- 基于 Spring Boot + Next.js 构建全栈系统
- 实现工具调用、RAG、异步任务流
- 完成 Docker 部署、日志监控、权限设计
- 支持多轮对话、上下文管理、会话存储

---

# 十四、一句话版学习顺序

如果只记住一条主线，就记这个：

1. 先学 TS + React + Next.js
2. 再回顾 Java + Spring Boot + MySQL
3. 再接 LLM API + Tool Calling + RAG
4. 最后补 Redis + Docker + Linux + Nginx

---

# 十五、下一步建议

如果你后续要继续深挖，可以继续拆成 3 份配套文件：

1. `3个月详细学习计划.md`
2. `第一个Agent全栈项目实战方案.md`
3. `Agent全栈工程师面试知识点.md`

建议顺序：
- 先按本文件明确全局地图
- 再做逐周学习计划
- 再开干项目实战

---

# 十六、给你的最终建议

你不是从零转行，而是在升级：
- 从移动端工程师
- 升级为能做 AI 产品落地的全栈工程师

路径上最重要的不是“学全”，而是：
- 快速补关键基础
- 尽快做出作品
- 用项目把知识串起来

先做出来，再补系统性。  
这是你这个背景下效率最高的路线。
