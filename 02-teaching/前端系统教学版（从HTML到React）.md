# 前端系统教学版（从 HTML 到 React）

> 目标：把你从“会看一点前端代码”带到“能独立做一个 Agent Web 前端”。  
> 适合对象：有 iOS 开发经验，但对 Web 前端、React、Next.js 不系统。  
> 阅读方式：这不是速查表，而是教材式内容。建议按章节读，并配合一个真实项目边学边做。

---

# 第一章：前端到底在做什么

很多移动端工程师第一次学前端时会觉得乱，因为前端同时出现了：
- HTML
- CSS
- JavaScript
- TypeScript
- React
- Next.js

看起来像一堆技术堆在一起。

其实你可以把它理解成分层：

## 1. HTML：结构层
它定义页面上“有什么”。

比如：
- 一个标题
- 一个输入框
- 一个按钮
- 一个消息列表

## 2. CSS：样式层
它定义页面“长什么样”。

比如：
- 字体大小
- 颜色
- 间距
- 边框
- 布局

## 3. JavaScript：逻辑层
它定义页面“怎么动”。

比如：
- 点按钮后发请求
- 输入框内容变化
- 收到接口结果后更新页面

## 4. React：组件化 UI 框架
它帮你把复杂页面组织成可维护的组件树。

## 5. Next.js：React 工程框架
它帮你用更工程化的方式组织前端项目。

所以前端不是 5 个世界，而是一个世界的 5 个层次。

---

# 第二章：HTML——页面结构的语言

## 2.1 HTML 的本质

HTML 不是编程语言，它更像结构描述语言。

你可以把它理解为：
- 我这里有一个区域
- 区域里面有标题
- 下面有输入框和按钮

例如：

```html
<div>
  <h1>Agent Chat</h1>
  <input placeholder="请输入消息" />
  <button>发送</button>
</div>
```

它只是告诉浏览器：页面里有什么。

---

## 2.2 最常用标签

### 1. div
最通用的块级容器。

```html
<div>这是一个区域</div>
```

在真实项目里，绝大多数布局都是一层层 `div` 叠起来的。

### 2. span
用于包一小段行内文本。

```html
<span>用户名</span>
```

### 3. 标题与段落
```html
<h1>大标题</h1>
<h2>小标题</h2>
<p>这是一段正文</p>
```

### 4. 输入相关
```html
<input />
<textarea></textarea>
<button>提交</button>
```

### 5. 列表
```html
<ul>
  <li>第一项</li>
  <li>第二项</li>
</ul>
```

### 6. 图片与链接
```html
<img src="avatar.png" />
<a href="/chat">进入聊天</a>
```

---

## 2.3 表单是什么

登录页、搜索框、聊天输入框，本质都属于表单交互。

```html
<form>
  <label>用户名</label>
  <input />
  <label>密码</label>
  <input type="password" />
  <button type="submit">登录</button>
</form>
```

你当前阶段不必在 HTML 上学得太深，重点是：
- 看得懂页面结构
- 会自己写基本页面骨架

---

# 第三章：CSS——页面为什么会变好看

## 3.1 CSS 的本质

CSS 负责样式和布局。它不是“装饰品”，而是页面体验的核心组成部分。

如果没有 CSS，页面就只是一堆排版很丑的文字和按钮。

---

## 3.2 盒模型

每一个元素都可以看成一个盒子，由以下几部分组成：
- content
- padding
- border
- margin

```css
.box {
  width: 200px;
  padding: 12px;
  border: 1px solid #ddd;
  margin: 16px;
}
```

### 你要建立的认知
前端布局问题，很多都可以回到盒模型来理解。

例如：
- 为什么两个元素挤在一起？
- 为什么内容贴边？
- 为什么这个盒子看起来不对？

大概率和 padding / margin / width / border 有关。

---

## 3.3 display

`display` 决定元素如何参与布局。

常见值：
- `block`
- `inline`
- `inline-block`
- `flex`

你当前最重要的是 `flex`。

---

## 3.4 Flex 布局

这是现代 Web 页面最重要的布局方式之一。

### 基本用法
```css
.container {
  display: flex;
}
```

### 主轴方向
```css
flex-direction: row;
flex-direction: column;
```

- `row`：横着排
- `column`：竖着排

### 主轴对齐
```css
justify-content: flex-start;
justify-content: center;
justify-content: space-between;
```

### 交叉轴对齐
```css
align-items: flex-start;
align-items: center;
align-items: stretch;
```

### 间距
```css
gap: 8px;
```

### 占满剩余空间
```css
flex: 1;
```

---

## 3.5 用 Flex 做聊天页面

一个典型聊天页：
- 左侧会话栏
- 右侧聊天区

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
  display: flex;
  flex-direction: column;
}

.messages {
  flex: 1;
  overflow-y: auto;
}

.input-area {
  display: flex;
  gap: 8px;
  padding: 12px;
}
```

这就是典型的 Web 页面布局思维。

---

## 3.6 常见 CSS 属性

### 尺寸
```css
width: 100%;
height: 100vh;
max-width: 800px;
```

### 间距
```css
margin: 16px;
padding: 12px;
```

### 文字
```css
font-size: 14px;
font-weight: 500;
line-height: 1.6;
color: #333;
```

### 背景和边框
```css
background: #fff;
border: 1px solid #eee;
border-radius: 8px;
```

### 阴影
```css
box-shadow: 0 2px 8px rgba(0,0,0,0.08);
```

---

# 第四章：JavaScript——前端页面为什么会“活起来”

## 4.1 JS 的作用

如果 HTML 是骨架，CSS 是外观，那么 JS 就是神经系统。

它负责：
- 处理事件
- 改变数据
- 发起请求
- 更新界面

---

## 4.2 变量、函数、对象、数组

### 变量
```js
let count = 0
const name = 'Tom'
```

### 函数
```js
function add(a, b) {
  return a + b
}
```

### 箭头函数
```js
const add2 = (a, b) => a + b
```

### 对象
```js
const user = {
  id: 1,
  name: 'Tom'
}
```

### 数组
```js
const messages = ['hello', 'world']
```

---

## 4.3 数组方法

这是你写 React 时会高频使用的。

### map
```js
const nums = [1, 2, 3]
const result = nums.map(item => item * 2)
```

### filter
```js
const result = nums.filter(item => item > 1)
```

### find
```js
const result = nums.find(item => item === 2)
```

### 为什么重要
因为 React 渲染列表时，本质就是把数据 `map` 成 UI。

---

## 4.4 异步编程

前端调用接口，本质是异步。

### Promise
先知道它表示“未来某个时刻会有结果”。

### async / await
```js
async function loadUser() {
  const res = await fetch('/api/user')
  const data = await res.json()
  return data
}
```

### 你必须真正理解
- 前端不会同步等待接口完成
- 所以页面通常要有 loading 状态
- 错误也要有 error 状态

---

## 4.5 常见易错点

### `===` 和 `==`
优先用 `===`

### null 和 undefined
不一样。

### 浅拷贝和直接修改
在 React 里，数组和对象更新时尽量返回新值，而不是直接改原值。

---

# 第五章：TypeScript——让前端代码可维护

## 5.1 为什么要用 TS

项目一大，纯 JS 容易乱。TS 的价值是：
- 提前发现类型错误
- 让代码更自解释
- 让多人协作更稳

---

## 5.2 基本类型

```ts
let name: string = 'Tom'
let age: number = 18
let ok: boolean = true
```

---

## 5.3 interface 与 type

### interface
适合定义对象结构。

```ts
interface User {
  id: number
  name: string
}
```

### type
适合定义联合类型、别名。

```ts
type Role = 'user' | 'assistant'
```

### 项目中怎么用
```ts
interface Message {
  id: string
  role: 'user' | 'assistant'
  content: string
}
```

---

## 5.4 泛型

```ts
interface ApiResponse<T> {
  code: number
  message: string
  data: T
}
```

### 你不需要一开始学太深
先知道：
- 泛型 = 可复用的类型占位符
- 常用于接口响应和通用函数

---

# 第六章：React——组件化前端的核心

## 6.1 React 的核心思想

React 的本质就是：
**UI = 状态的函数**

意思是：
- 你维护数据状态
- React 根据状态渲染界面
- 状态变化，界面自动更新

---

## 6.2 组件

```tsx
function Hello() {
  return <div>Hello</div>
}
```

组件就是可以复用的 UI 单元。

在聊天页面里，你会拆成：
- `Sidebar`
- `ConversationList`
- `MessageList`
- `ChatInput`

---

## 6.3 props

props 是父组件传给子组件的数据。

```tsx
function MessageBubble({ content }: { content: string }) {
  return <div>{content}</div>
}
```

---

## 6.4 state 和 useState

```tsx
const [input, setInput] = useState('')
```

### 常见状态
- 输入框内容
- 会话列表
- 当前消息列表
- loading
- 当前会话 id

### 更新数组示例
```tsx
setMessages(prev => [...prev, newMessage])
```

---

## 6.5 useEffect

最常见用途：页面加载后请求数据。

```tsx
useEffect(() => {
  loadConversations()
}, [])
```

### 你要理解
- 它常用于副作用
- 不要把一切逻辑都堆进 useEffect

---

## 6.6 列表渲染和条件渲染

### 列表渲染
```tsx
{messages.map(msg => (
  <div key={msg.id}>{msg.content}</div>
))}
```

### 条件渲染
```tsx
{loading ? <div>加载中...</div> : <MessageList />}
```

---

## 6.7 表单与事件

### 输入框
```tsx
<input value={input} onChange={e => setInput(e.target.value)} />
```

### 按钮点击
```tsx
<button onClick={handleSend}>发送</button>
```

---

# 第七章：Next.js——把 React 做成真正项目

## 7.1 为什么要用 Next.js

因为它比“纯 React + 自己搭工程”更适合快速做项目。

### 你当前重点掌握
- 项目结构
- 路由
- 页面组织
- 客户端组件

---

## 7.2 App Router

例如：

```text
app/
  login/
    page.tsx
  chat/
    page.tsx
```

对应：
- `/login`
- `/chat`

---

## 7.3 `use client`

当组件需要：
- useState
- useEffect
- onClick
- 浏览器 API

就加：

```tsx
'use client'
```

---

## 7.4 前端项目怎么拆

建议：

```text
src/
  app/
  components/
  services/
  hooks/
  types/
  utils/
```

### 各目录职责
- `app/`：页面
- `components/`：组件
- `services/`：请求
- `hooks/`：复用逻辑
- `types/`：类型定义
- `utils/`：工具函数

---

# 第八章：前端如何和后端通信

## 8.1 HTTP 请求基础

前端通过 HTTP 请求和后端交互。

### 常见方法
- GET：查数据
- POST：新建 / 提交
- PUT：更新
- DELETE：删除

---

## 8.2 fetch 基本用法

```ts
const res = await fetch('/api/user')
const data = await res.json()
```

### POST JSON
```ts
await fetch('/api/chat/send', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ content: '你好' })
})
```

---

## 8.3 为什么要封装请求层

因为实际项目中你会需要：
- 统一 base URL
- 统一 token
- 统一错误处理

---

# 第九章：如何做一个聊天前端

## 9.1 页面结构

一个最小聊天页通常包括：
- 左侧会话列表
- 右侧消息区
- 底部输入框

## 9.2 状态设计

你至少要有：

```ts
const [conversations, setConversations] = useState<Conversation[]>([])
const [messages, setMessages] = useState<Message[]>([])
const [currentConversationId, setCurrentConversationId] = useState<string | null>(null)
const [input, setInput] = useState('')
const [loading, setLoading] = useState(false)
```

## 9.3 发送消息流程

1. 用户输入内容
2. 更新本地消息列表（可选）
3. 调用后端接口
4. 拿到回复
5. 更新消息列表

---

# 第十章：当前端出了问题，怎么排查

## 10.1 看浏览器控制台

错误往往先出现在 Console。

## 10.2 看 Network 面板

重点看：
- 请求是否发出去
- 返回码是多少
- 返回内容是什么

## 10.3 常见错误

### map is not a function
说明你以为是数组，实际不是。

### Cannot read properties of undefined
说明对象还没准备好就取属性了。

### CORS 错误
后端没配跨域。

---

# 第十一章：你应该掌握到什么程度

这份教材学完后，你的目标不是成为资深前端，而是达到：

- 能独立搭一个 Next.js 前端
- 能写聊天页、登录页、上传页
- 能组织组件和状态
- 能调用后端接口
- 能看懂常见报错

做到这一步，你已经足够进入 Agent 前端实战。

---

# 第十二章：对你最重要的建议

作为 iOS 开发转前端，你最重要的不是“把所有前端概念学完”，而是：

1. 把 CSS Flex 学熟
2. 把 React 状态流学懂
3. 把接口调用和页面联动做顺
4. 通过一个聊天项目把知识串起来

只要这四件事跑通，你前端就会起飞。
