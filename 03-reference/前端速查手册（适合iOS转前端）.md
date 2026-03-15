# 前端速查手册（适合 iOS 转前端）

> 目标：不是系统讲理论，而是让你在学习和做项目时，遇到问题能快速翻到答案。  
> 适合对象：有 iOS 开发经验，正在补 Web 前端、React、Next.js。

---

# 一、先建立映射：iOS 和前端的对应关系

| iOS | 前端 |
|---|---|
| UIView / UIViewController | HTML + React 组件 |
| AutoLayout / StackView | CSS / Flex |
| 属性 | state / props |
| 网络请求 | fetch / axios |
| model | TypeScript interface/type |
| 页面跳转 | 路由 |
| 本地存储 | localStorage / cookie |

你不要把前端当成完全陌生的世界。很多概念只是换了壳。

---

# 二、HTML 速查

## 最常用标签

### 容器
```html
<div></div>
<span></span>
```

- `div`：块级容器，最常用
- `span`：行内容器，常包一小段文字

### 文本
```html
<h1>标题</h1>
<p>正文</p>
```

### 输入
```html
<input placeholder="请输入" />
<textarea></textarea>
<button>发送</button>
```

### 列表
```html
<ul>
  <li>会话1</li>
  <li>会话2</li>
</ul>
```

### 表单
```html
<form>
  <input />
  <button type="submit">提交</button>
</form>
```

## 什么时候用什么
- 页面结构：`div`
- 局部文字：`span`
- 输入：`input/textarea`
- 列表：`ul/li`
- 按钮：`button`

---

# 三、CSS 速查

## 1. 盒模型

```css
.box {
  width: 200px;
  padding: 12px;
  border: 1px solid #ddd;
  margin: 16px;
}
```

顺序：
- content
- padding
- border
- margin

## 2. Flex 布局

### 横向布局
```css
.row {
  display: flex;
  flex-direction: row;
}
```

### 纵向布局
```css
.column {
  display: flex;
  flex-direction: column;
}
```

### 主轴分布
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

## 3. 常见布局模板

### 左右布局
```css
.page {
  display: flex;
  height: 100vh;
}

.sidebar {
  width: 260px;
}

.main {
  flex: 1;
}
```

### 顶部 + 内容 + 底部
```css
.page {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.content {
  flex: 1;
}
```

### 输入区固定底部
```css
.input-area {
  position: sticky;
  bottom: 0;
  background: white;
}
```

## 4. 常见样式
```css
color: #333;
background: #fff;
border-radius: 8px;
box-shadow: 0 2px 8px rgba(0,0,0,0.08);
font-size: 14px;
font-weight: 500;
```

---

# 四、JavaScript 速查

## 1. 变量
```js
let count = 0
const name = 'Tom'
```

- `let`：可变
- `const`：不可重新赋值，优先用它

## 2. 函数
```js
function add(a, b) {
  return a + b
}

const add2 = (a, b) => a + b
```

## 3. 对象
```js
const user = {
  id: 1,
  name: 'Tom'
}

console.log(user.name)
```

## 4. 数组
```js
const list = [1, 2, 3]
```

### map
```js
const result = list.map(item => item * 2)
```

### filter
```js
const result = list.filter(item => item > 1)
```

### find
```js
const result = list.find(item => item === 2)
```

## 5. 条件判断
```js
if (count > 0) {
  console.log('positive')
} else {
  console.log('zero')
}
```

## 6. 异步
```js
async function loadData() {
  const res = await fetch('/api/users')
  const data = await res.json()
  return data
}
```

## 7. 常见坑
- 优先用 `===` 不用 `==`
- `null` 和 `undefined` 不一样
- 不要直接改原对象或原数组

---

# 五、TypeScript 速查

## 1. 基本类型
```ts
let name: string = 'Tom'
let age: number = 18
let ok: boolean = true
```

## 2. 接口
```ts
interface User {
  id: number
  name: string
}
```

## 3. 类型别名
```ts
type Role = 'user' | 'assistant'
```

## 4. 业务对象示例
```ts
interface Message {
  id: string
  role: 'user' | 'assistant'
  content: string
}
```

## 5. 泛型
```ts
interface ApiResponse<T> {
  code: number
  message: string
  data: T
}
```

## 6. 可选属性
```ts
interface User {
  id: number
  nickname?: string
}
```

---

# 六、React 速查

## 1. 组件
```tsx
function Hello() {
  return <div>Hello</div>
}
```

## 2. props
```tsx
function MessageBubble({ content }: { content: string }) {
  return <div>{content}</div>
}
```

## 3. useState
```tsx
const [count, setCount] = useState(0)
```

更新：
```tsx
setCount(count + 1)
```

## 4. useEffect
```tsx
useEffect(() => {
  console.log('页面加载后执行')
}, [])
```

## 5. 输入框双向绑定
```tsx
const [value, setValue] = useState('')

<input value={value} onChange={e => setValue(e.target.value)} />
```

## 6. 列表渲染
```tsx
{messages.map(msg => (
  <div key={msg.id}>{msg.content}</div>
))}
```

## 7. 条件渲染
```tsx
{loading ? <div>加载中</div> : <div>完成</div>}
```

## 8. 点击事件
```tsx
<button onClick={handleSend}>发送</button>
```

---

# 七、Next.js 速查

## 1. 常见目录
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

## 2. 页面文件
`page.tsx` 就是一个页面。

## 3. 公共布局
`layout.tsx` 放页面公共结构。

## 4. 什么时候加 `use client`
当你要：
- useState
- useEffect
- onClick
- onChange

就要把组件标成客户端组件：

```tsx
'use client'
```

## 5. 环境变量
```env
NEXT_PUBLIC_API_BASE_URL=http://localhost:8080
```

---

# 八、请求封装速查

## 1. 最小 fetch 封装
```ts
export async function request(url: string, options?: RequestInit) {
  const res = await fetch(url, options)
  if (!res.ok) {
    throw new Error('request failed')
  }
  return res.json()
}
```

## 2. POST JSON
```ts
await request('/api/chat/send', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ content: '你好' })
})
```

## 3. 带 token
```ts
headers: {
  'Content-Type': 'application/json',
  'Authorization': `Bearer ${token}`
}
```

---

# 九、聊天页最小结构速查

## 页面拆分建议
- `Sidebar`
- `ConversationList`
- `ChatWindow`
- `MessageList`
- `ChatInput`

## 最小消息类型
```ts
interface Message {
  id: string
  role: 'user' | 'assistant'
  content: string
}
```

## 最小页面状态
```ts
const [messages, setMessages] = useState<Message[]>([])
const [input, setInput] = useState('')
const [loading, setLoading] = useState(false)
```

---

# 十、前端常见报错速查

## 1. map is not a function
原因：你以为是数组，实际不是。

先打印：
```ts
console.log(data)
```

## 2. Cannot read properties of undefined
原因：对象还没拿到就取属性。

处理：
- 判空
- 可选链 `user?.name`

## 3. Hydration 错误
常见于 Next.js 服务端和客户端渲染不一致。

先记结论：
- 有状态、事件、浏览器 API 的组件，尽量用 `use client`

## 4. CORS 报错
原因：前端和后端端口不同，后端没配跨域。

---

# 十一、你当前阶段最该掌握到什么程度

如果你达到下面这些，就够进入 Agent 项目实战了：

- 能写一个聊天页 UI
- 能用 React 管理输入框和消息列表
- 能用 Next.js 组织项目
- 能调用后端接口
- 能看懂 TypeScript 类型定义
- 能定位基本前端报错

---

# 十二、给你的实用建议

作为 iOS 开发转前端，你最容易卡在两件事：

## 1. CSS 布局
解决方案：死磕 Flex，先别在花哨样式上耗太久。

## 2. React 状态流
解决方案：反复问自己：
- 这个数据是谁持有？
- 谁修改它？
- 谁展示它？

把这两个搞懂，你前端就会进步很快。
