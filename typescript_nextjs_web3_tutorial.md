# 50天TypeScript + Next.js 15 + Web3.0精通教程

## 📚 课程概述
本教程分为三个主要阶段，循序渐进地掌握现代Web3开发技术栈。

---

## 第一阶段：TypeScript基础 (Day 1-15)

### Day 1: TypeScript环境搭建与基础类型
**知识点：**
- TypeScript安装与配置
- 基础类型：string, number, boolean, null, undefined
- 类型注解与类型推断

**代码示例：**
```typescript
// 安装: npm install -g typescript
// 初始化: tsc --init

// 基础类型
let username: string = "Alice";
let age: number = 25;
let isActive: boolean = true;

// 类型推断
let inferredString = "Hello"; // 自动推断为string

// 函数类型注解
function greet(name: string): string {
  return `Hello, ${name}!`;
}

console.log(greet("TypeScript"));
```

**练习项目：** 创建一个简单的用户信息管理程序

---

### Day 2: 数组、元组与枚举
**知识点：**
- 数组类型定义
- 元组(Tuple)的使用
- 枚举(Enum)类型

**代码示例：**
```typescript
// 数组
let numbers: number[] = [1, 2, 3, 4, 5];
let strings: Array<string> = ["a", "b", "c"];

// 元组
let user: [string, number, boolean] = ["Alice", 25, true];

// 枚举
enum UserRole {
  Admin = "ADMIN",
  User = "USER",
  Guest = "GUEST"
}

function checkPermission(role: UserRole): boolean {
  return role === UserRole.Admin;
}

console.log(checkPermission(UserRole.Admin)); // true
```

**练习项目：** 创建一个任务管理系统，使用枚举定义任务状态

---

### Day 3: 接口(Interface)
**知识点：**
- 接口定义与使用
- 可选属性与只读属性
- 接口继承

**代码示例：**
```typescript
// 基础接口
interface User {
  id: number;
  name: string;
  email: string;
  age?: number; // 可选属性
  readonly createdAt: Date; // 只读属性
}

// 接口继承
interface Admin extends User {
  permissions: string[];
  role: "admin";
}

const admin: Admin = {
  id: 1,
  name: "Admin User",
  email: "admin@example.com",
  createdAt: new Date(),
  permissions: ["read", "write", "delete"],
  role: "admin"
};

// 函数接口
interface SearchFunc {
  (source: string, subString: string): boolean;
}

const mySearch: SearchFunc = (src, sub) => {
  return src.includes(sub);
};
```

**练习项目：** 设计一个电商系统的Product和Order接口

---

### Day 4: 类(Class)基础
**知识点：**
- 类的定义与实例化
- 构造函数
- 访问修饰符(public, private, protected)

**代码示例：**
```typescript
class User {
  private id: number;
  public name: string;
  protected email: string;

  constructor(id: number, name: string, email: string) {
    this.id = id;
    this.name = name;
    this.email = email;
  }

  public getInfo(): string {
    return `${this.name} (${this.email})`;
  }

  private validateEmail(): boolean {
    return this.email.includes("@");
  }
}

class AdminUser extends User {
  private permissions: string[];

  constructor(id: number, name: string, email: string, permissions: string[]) {
    super(id, name, email);
    this.permissions = permissions;
  }

  public getPermissions(): string[] {
    return this.permissions;
  }
}

const admin = new AdminUser(1, "Admin", "admin@test.com", ["read", "write"]);
console.log(admin.getInfo());
```

**练习项目：** 创建一个简单的银行账户管理系统

---

### Day 5: 泛型(Generics)
**知识点：**
- 泛型函数
- 泛型接口
- 泛型类
- 泛型约束

**代码示例：**
```typescript
// 泛型函数
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("Hello");
let output2 = identity<number>(123);

// 泛型接口
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

interface User {
  id: number;
  name: string;
}

const userResponse: ApiResponse<User> = {
  data: { id: 1, name: "Alice" },
  status: 200,
  message: "Success"
};

// 泛型类
class DataStore<T> {
  private data: T[] = [];

  add(item: T): void {
    this.data.push(item);
  }

  getAll(): T[] {
    return this.data;
  }
}

const userStore = new DataStore<User>();
userStore.add({ id: 1, name: "Alice" });

// 泛型约束
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}

logLength("Hello"); // OK
logLength([1, 2, 3]); // OK
```

**练习项目：** 创建一个通用的数据存储类，支持CRUD操作

---

### Day 6: 高级类型 - Union与Intersection
**知识点：**
- 联合类型(Union Types)
- 交叉类型(Intersection Types)
- 类型守卫(Type Guards)

**代码示例：**
```typescript
// 联合类型
type Status = "pending" | "approved" | "rejected";

function updateStatus(status: Status): void {
  console.log(`Status updated to: ${status}`);
}

updateStatus("approved"); // OK
// updateStatus("invalid"); // Error

// 交叉类型
interface Person {
  name: string;
  age: number;
}

interface Employee {
  employeeId: number;
  department: string;
}

type Staff = Person & Employee;

const staff: Staff = {
  name: "John",
  age: 30,
  employeeId: 123,
  department: "IT"
};

// 类型守卫
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function processValue(value: string | number): void {
  if (isString(value)) {
    console.log(value.toUpperCase());
  } else {
    console.log(value.toFixed(2));
  }
}
```

**练习项目：** 创建一个支付系统，处理多种支付方式

---

### Day 7: 类型别名与字面量类型
**知识点：**
- Type Alias
- 字面量类型
- 模板字面量类型

**代码示例：**
```typescript
// 类型别名
type ID = string | number;
type User = {
  id: ID;
  name: string;
  email: string;
};

// 字面量类型
type Direction = "north" | "south" | "east" | "west";
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";

function sendRequest(url: string, method: HttpMethod): void {
  console.log(`Sending ${method} request to ${url}`);
}

// 模板字面量类型
type EventName = "click" | "scroll" | "mousemove";
type EventHandler = `on${Capitalize<EventName>}`;
// 结果: "onClick" | "onScroll" | "onMousemove"

type Color = "red" | "blue" | "green";
type Size = "small" | "medium" | "large";
type Style = `${Color}-${Size}`;
// 结果: "red-small" | "red-medium" | ... (9种组合)

const style: Style = "red-small";
```

**练习项目：** 创建一个API路由类型系统

---

### Day 8: 类型推断与类型断言
**知识点：**
- 类型推断机制
- 类型断言(as语法)
- 非空断言操作符(!)

**代码示例：**
```typescript
// 类型推断
let x = 3; // 推断为number
let arr = [1, 2, 3]; // 推断为number[]

function createUser(name: string, age: number) {
  return { name, age, createdAt: new Date() };
}
// 返回类型被推断为 { name: string; age: number; createdAt: Date; }

// 类型断言
const canvas = document.getElementById("canvas") as HTMLCanvasElement;
canvas.getContext("2d");

// 双重断言(谨慎使用)
const value = "Hello" as unknown as number; // 不推荐

// 非空断言
function processUser(user: User | null) {
  console.log(user!.name); // 断言user不为null
}

// const断言
const config = {
  apiUrl: "https://api.example.com",
  timeout: 5000
} as const;
// config的类型为 { readonly apiUrl: "https://api.example.com"; readonly timeout: 5000; }
```

**练习项目：** 创建一个DOM操作工具库

---

### Day 9: 函数重载与可选参数
**知识点：**
- 函数重载
- 可选参数与默认参数
- 剩余参数

**代码示例：**
```typescript
// 函数重载
function createDate(timestamp: number): Date;
function createDate(year: number, month: number, day: number): Date;
function createDate(yearOrTimestamp: number, month?: number, day?: number): Date {
  if (month !== undefined && day !== undefined) {
    return new Date(yearOrTimestamp, month - 1, day);
  }
  return new Date(yearOrTimestamp);
}

const date1 = createDate(1000000000000);
const date2 = createDate(2024, 1, 1);

// 可选参数与默认参数
function buildUrl(protocol: string = "https", domain: string, path?: string): string {
  const base = `${protocol}://${domain}`;
  return path ? `${base}/${path}` : base;
}

console.log(buildUrl("http", "example.com", "api/users"));

// 剩余参数
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}

console.log(sum(1, 2, 3, 4, 5)); // 15

// 函数类型
type MathOperation = (a: number, b: number) => number;

const add: MathOperation = (a, b) => a + b;
const multiply: MathOperation = (a, b) => a * b;
```

**练习项目：** 创建一个数学计算库

---

### Day 10: 装饰器(Decorators)
**知识点：**
- 类装饰器
- 方法装饰器
- 属性装饰器
- 参数装饰器

**代码示例：**
```typescript
// 需要在tsconfig.json中启用: "experimentalDecorators": true

// 类装饰器
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

@sealed
class BugReport {
  type = "report";
  title: string;

  constructor(title: string) {
    this.title = title;
  }
}

// 方法装饰器
function log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Calling ${propertyKey} with args:`, args);
    const result = originalMethod.apply(this, args);
    console.log(`Result:`, result);
    return result;
  };

  return descriptor;
}

class Calculator {
  @log
  add(a: number, b: number): number {
    return a + b;
  }
}

const calc = new Calculator();
calc.add(2, 3);

// 属性装饰器
function readonly(target: any, propertyKey: string) {
  Object.defineProperty(target, propertyKey, {
    writable: false
  });
}

class User {
  @readonly
  id: number = 1;
}
```

**练习项目：** 创建一个日志系统，使用装饰器记录方法调用

---

### Day 11: 模块系统
**知识点：**
- ES6模块导入导出
- 命名空间
- 模块解析策略

**代码示例：**
```typescript
// math.ts - 导出
export function add(a: number, b: number): number {
  return a + b;
}

export function subtract(a: number, b: number): number {
  return a - b;
}

export const PI = 3.14159;

export default class Calculator {
  multiply(a: number, b: number): number {
    return a * b;
  }
}

// main.ts - 导入
import Calculator, { add, subtract, PI } from './math';
import * as MathUtils from './math';

const calc = new Calculator();
console.log(calc.multiply(5, 3));
console.log(add(10, 5));
console.log(MathUtils.PI);

// 命名空间
namespace Validation {
  export interface StringValidator {
    isValid(s: string): boolean;
  }

  export class EmailValidator implements StringValidator {
    isValid(s: string): boolean {
      return s.includes("@");
    }
  }
}

const emailValidator = new Validation.EmailValidator();
console.log(emailValidator.isValid("test@example.com"));

// 类型导入导出
// types.ts
export interface User {
  id: number;
  name: string;
}

export type UserRole = "admin" | "user";

// app.ts
import type { User, UserRole } from './types';
```

**练习项目：** 创建一个模块化的工具库

---

### Day 12: 异步编程与Promise
**知识点：**
- Promise类型定义
- async/await
- 错误处理

**代码示例：**
```typescript
// Promise基础
function fetchUser(id: number): Promise<User> {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) {
        resolve({ id, name: "Alice", email: "alice@example.com" });
      } else {
        reject(new Error("Invalid user ID"));
      }
    }, 1000);
  });
}

// async/await
async function getUser(id: number): Promise<User> {
  try {
    const user = await fetchUser(id);
    console.log("User fetched:", user);
    return user;
  } catch (error) {
    console.error("Error fetching user:", error);
    throw error;
  }
}

// 并行请求
async function fetchMultipleUsers(ids: number[]): Promise<User[]> {
  const promises = ids.map(id => fetchUser(id));
  return Promise.all(promises);
}

// 自定义异步函数类型
type AsyncFunction<T> = () => Promise<T>;

const getData: AsyncFunction<string> = async () => {
  return "Data loaded";
};

// 带泛型的API函数
interface ApiResponse<T> {
  data: T;
  status: number;
}

async function apiRequest<T>(url: string): Promise<ApiResponse<T>> {
  const response = await fetch(url);
  const data = await response.json();
  return {
    data,
    status: response.status
  };
}
```

**练习项目：** 创建一个异步数据获取工具

---

### Day 13: 实用工具类型
**知识点：**
- Partial, Required, Readonly
- Pick, Omit, Exclude, Extract
- Record, ReturnType, Parameters

**代码示例：**
```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}

// Partial - 所有属性变为可选
type PartialUser = Partial<User>;
const user1: PartialUser = { name: "Alice" };

// Required - 所有属性变为必需
type RequiredUser = Required<User>;

// Readonly - 所有属性变为只读
type ReadonlyUser = Readonly<User>;
const user2: ReadonlyUser = { id: 1, name: "Bob", email: "bob@test.com", age: 25 };
// user2.name = "Charlie"; // Error

// Pick - 选择特定属性
type UserPreview = Pick<User, "id" | "name">;
const preview: UserPreview = { id: 1, name: "Alice" };

// Omit - 排除特定属性
type UserWithoutEmail = Omit<User, "email">;

// Record - 创建对象类型
type UserRoles = Record<string, string[]>;
const roles: UserRoles = {
  admin: ["read", "write", "delete"],
  user: ["read"]
};

// ReturnType - 获取函数返回类型
function createUser() {
  return { id: 1, name: "Alice" };
}
type UserType = ReturnType<typeof createUser>;

// Parameters - 获取函数参数类型
function updateUser(id: number, name: string, age: number) {}
type UpdateUserParams = Parameters<typeof updateUser>;
// [number, string, number]

// Exclude - 从联合类型中排除
type T1 = Exclude<"a" | "b" | "c", "a">; // "b" | "c"

// Extract - 从联合类型中提取
type T2 = Extract<"a" | "b" | "c", "a" | "f">; // "a"

// NonNullable - 排除null和undefined
type T3 = NonNullable<string | number | undefined>; // string | number
```

**练习项目：** 创建一个表单验证系统，使用工具类型

---

### Day 14: 条件类型与映射类型
**知识点：**
- 条件类型
- 映射类型
- infer关键字

**代码示例：**
```typescript
// 条件类型
type IsString<T> = T extends string ? true : false;
type Test1 = IsString<string>; // true
type Test2 = IsString<number>; // false

// 实用条件类型
type NonNullable<T> = T extends null | undefined ? never : T;
type Result = NonNullable<string | null | undefined>; // string

// 映射类型
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Optional<T> = {
  [P in keyof T]?: T[P];
};

interface User {
  id: number;
  name: string;
}

type ReadonlyUser = Readonly<User>;
type OptionalUser = Optional<User>;

// 高级映射类型
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

type UserGetters = Getters<User>;
// { getId: () => number; getName: () => string; }

// infer关键字
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
type ArrayElement<T> = T extends (infer E)[] ? E : never;

type StringArray = string[];
type ElementType = ArrayElement<StringArray>; // string

// 递归条件类型
type DeepReadonly<T> = {
  readonly [P in keyof T]: T[P] extends object ? DeepReadonly<T[P]> : T[P];
};

interface NestedUser {
  id: number;
  profile: {
    name: string;
    address: {
      city: string;
    };
  };
}

type DeepReadonlyUser = DeepReadonly<NestedUser>;
```

**练习项目：** 创建一个类型安全的状态管理库

---

### Day 15: TypeScript配置与最佳实践
**知识点：**
- tsconfig.json配置
- 严格模式
- 代码组织最佳实践
- 类型声明文件(.d.ts)

**代码示例：**
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "lib": ["ES2020", "DOM"],
    "jsx": "react-jsx",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "incremental": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@components/*": ["src/components/*"],
      "@utils/*": ["src/utils/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

```typescript
// types/global.d.ts - 全局类型声明
declare global {
  interface Window {
    ethereum?: any;
  }
}

export {};

// types/api.d.ts - API类型声明
declare module 'my-api-library' {
  export function fetchData<T>(url: string): Promise<T>;
}

// 最佳实践示例
// 使用严格的null检查
function processUser(user: User | null): string {
  if (!user) {
    return "No user";
  }
  return user.name;
}

// 避免使用any
function badExample(data: any) { // 不推荐
  return data.value;
}

function goodExample(data: unknown): string {
  if (typeof data === "object" && data !== null && "value" in data) {
    return String(data.value);
  }
  return "";
}

// 使用类型守卫
interface Cat {
  meow(): void;
}

interface Dog {
  bark(): void;
}

function isCat(animal: Cat | Dog): animal is Cat {
  return "meow" in animal;
}

function makeSound(animal: Cat | Dog): void {
  if (isCat(animal)) {
    animal.meow();
  } else {
    animal.bark();
  }
}
```

**项目实战：** 构建一个完整的TypeScript项目模板

---

## 第二阶段：Next.js 15基础与进阶 (Day 16-35)

### Day 16: Next.js 15环境搭建与项目结构
**知识点：**
- Next.js 15安装与配置
- App Router vs Pages Router
- 项目目录结构
- TypeScript集成

**代码示例：**
```bash
# 创建Next.js项目
npx create-next-app@latest my-next-app --typescript --tailwind --app

# 项目结构
my-next-app/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   └── globals.css
├── public/
├── components/
├── lib/
├── types/
├── next.config.js
├── tsconfig.json
└── package.json
```

```typescript
// app/layout.tsx
import type { Metadata } from 'next';
import { Inter } from 'next/font/google';
import './globals.css';

const inter = Inter({ subsets: ['latin'] });

export const metadata: Metadata = {
  title: 'My Next.js App',
  description: 'Built with Next.js 15',
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={inter.className}>{children}</body>
    </html>
  );
}

// app/page.tsx
export default function Home() {
  return (
    <main className="flex min-h-screen flex-col items-center justify-center p-24">
      <h1 className="text-4xl font-bold">Welcome to Next.js 15</h1>
    </main>
  );
}

// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  swcMinify: true,
  images: {
    domains: ['example.com'],
  },
};

module.exports = nextConfig;
```

**练习项目：** 创建一个基础的Next.js应用

---

### Day 17: 路由系统与导航
**知识点：**
- App Router基础
- 动态路由
- 路由组
- Link组件与useRouter

**代码示例：**
```typescript
// app/about/page.tsx
export default function AboutPage() {
  return <h1>About Page</h1>;
}

// app/blog/[slug]/page.tsx - 动态路由
interface PageProps {
  params: { slug: string };
}

export default function BlogPost({ params }: PageProps) {
  return <h1>Blog Post: {params.slug}</h1>;
}

// app/blog/[...slug]/page.tsx - 捕获所有路由
export default function CatchAll({ params }: { params: { slug: string[] } }) {
  return <div>Segments: {params.slug.join('/')}</div>;
}

// components/Navigation.tsx
'use client';

import Link from 'next/link';
import { useRouter, usePathname } from 'next/navigation';

export default function Navigation() {
  const router = useRouter();
  const pathname = usePathname();

  const handleNavigate = () => {
    router.push('/about');
  };

  return (
    <nav className="flex gap-4 p-4">
      <Link 
        href="/" 
        className={pathname === '/' ? 'font-bold' : ''}
      >
        Home
      </Link>
      <Link 
        href="/about"
        className={pathname === '/about' ? 'font-bold' : ''}
      >
        About
      </Link>
      <Link href="/blog/first-post">Blog</Link>
      <button onClick={handleNavigate}>Navigate to About</button>
    </nav>
  );
}

// 路由组 - app/(marketing)/layout.tsx
export default function MarketingLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <div className="marketing-layout">
      <header>Marketing Header</header>
      {children}
    </div>
  );
}
```

**练习项目：** 创建一个多页面博客应用

---

### Day 18: 服务器组件与客户端组件
**知识点：**
- Server Components
- Client Components
- 'use client'指令
- 组件组合模式

**代码示例：**
```typescript
// app/dashboard/page.tsx - 服务器组件(默认)
import { headers } from 'next/headers';

async function getData() {
  const res = await fetch('https://api.example.com/data', {
    cache: 'no-store' // 动态渲染
  });
  return res.json();
}

export default async function Dashboard() {
  const data = await getData();
  const headersList = headers();
  const userAgent = headersList.get('user-agent');

  return (
    <div>
      <h1>Dashboard</h1>
      <p>User Agent: {userAgent}</p>
      <DataDisplay data={data} />
    </div>
  );
}

// components/Counter.tsx - 客户端组件
'use client';

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}

// components/DataDisplay.tsx - 混合使用
'use client';

import { useState, useEffect } from 'react';

interface DataDisplayProps {
  data: any;
}

export default function DataDisplay({ data }: DataDisplayProps) {
  const [isExpanded, setIsExpanded] = useState(false);

  return (
    <div>
      <button onClick={() => setIsExpanded(!isExpanded)}>
        {isExpanded ? 'Collapse' : 'Expand'}
      </button>
      {isExpanded && <pre>{JSON.stringify(data, null, 2)}</pre>}
    </div>
  );
}

// 组件组合最佳实践
// app/products/page.tsx
import ClientComponent from '@/components/ClientComponent';
import ServerComponent from '@/components/ServerComponent';

export default function ProductsPage() {
  return (
    <div>
      <ServerComponent>
        {/* 将客户端组件作为children传递 */}
        <ClientComponent />
      </ServerComponent>
    </div>
  );
}
```

**练习项目：** 创建一个包含服务器和客户端组件的仪表板

---

### Day 19: 数据获取策略
**知识点：**
- fetch API扩展
- 缓存策略
- Revalidation
- Streaming与Suspense

**代码示例：**
```typescript
// lib/api.ts
export async function getStaticData() {
  const res = await fetch('https://api.example.com/data', {
    cache: 'force-cache' // 静态生成(默认)
  });
  return res.json();
}

export async function getDynamicData() {
  const res = await fetch('https://api.example.com/data', {
    cache: 'no-store' // 每次请求都获取新数据
  });
  return res.json();
}

export async function getRevalidatedData() {
  const res = await fetch('https://api.example.com/data', {
    next: { revalidate: 60 } // 60秒后重新验证
  });
  return res.json();
}

// 带标签的缓存
export async function getTaggedData() {
  const res = await fetch('https://api.example.com/data', {
    next: { 
      revalidate: 3600,
      tags: ['posts'] 
    }
  });
  return res.json();
}

// app/posts/page.tsx - 使用Suspense
import { Suspense } from 'react';

async function Posts() {
  const posts = await getStaticData();
  return (
    <ul>
      {posts.map((post: any) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

function PostsSkeleton() {
  return <div>Loading posts...</div>;
}

export default function PostsPage() {
  return (
    <div>
      <h1>Posts</h1>
      <Suspense fallback={<PostsSkeleton />}>
        <Posts />
      </Suspense>
    </div>
  );
}

// app/api/revalidate/route.ts - 手动重新验证
import { revalidateTag, revalidatePath } from 'next/cache';
import { NextRequest, NextResponse } from 'next/server';

export async function POST(request: NextRequest) {
  const tag = request.nextUrl.searchParams.get('tag');
  
  if (tag) {
    revalidateTag(tag);
  }
  
  revalidatePath('/posts');
  
  return NextResponse.json({ revalidated: true, now: Date.now() });
}

// 并行数据获取
async function getData1() {
  const res = await fetch('https://api.example.com/data1');
  return res.json();
}

async function getData2() {
  const res = await fetch('https://api.example.com/data2');
  return res.json();
}

export default async function ParallelPage() {
  const [data1, data2] = await Promise.all([
    getData1(),
    getData2()
  ]);

  return (
    <div>
      <div>{JSON.stringify(data1)}</div>
      <div>{JSON.stringify(data2)}</div>
    </div>
  );
}
```

**练习项目：** 创建一个新闻聚合应用，实现不同的缓存策略

---

### Day 20: Loading UI与Error Handling
**知识点：**
- loading.tsx
- error.tsx
- not-found.tsx
- 错误边界

**代码示例：**
```typescript
// app/dashboard/loading.tsx
export default function Loading() {
  return (
    <div className="flex items-center justify-center min-h-screen">
      <div className="animate-spin rounded-full h-32 w-32 border-b-2 border-gray-900"></div>
    </div>
  );
}

// app/dashboard/error.tsx
'use client';

import { useEffect } from 'react';

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  useEffect(() => {
    console.error(error);
  }, [error]);

  return (
    <div className="flex flex-col items-center justify-center min-h-screen">
      <h2 className="text-2xl font-bold mb-4">Something went wrong!</h2>
      <p className="mb-4">{error.message}</p>
      <button
        onClick={() => reset()}
        className="px-4 py-2 bg-blue-500 text-white rounded"
      >
        Try again
      </button>
    </div>
  );
}

// app/dashboard/not-found.tsx
import Link from 'next/link';

export default function NotFound() {
  return (
    <div className="flex flex-col items-center justify-center min-h-screen">
      <h2 className="text-4xl font-bold mb-4">404 - Not Found</h2>
      <p className="mb-4">Could not find requested resource</p>
      <Link href="/" className="text-blue-500 hover:underline">
        Return Home
      </Link>
    </div>
  );
}

// app/posts/[id]/page.tsx - 触发not-found
import { notFound } from 'next/navigation';

async function getPost(id: string) {
  const res = await fetch(`https://api.example.com/posts/${id}`);
  
  if (!res.ok) {
    return null;
  }
  
  return res.json();
}

export default async function PostPage({ 
  params 
}: { 
  params: { id: string } 
}) {
  const post = await getPost(params.id);

  if (!post) {
    notFound();
  }

  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}

// components/ErrorBoundary.tsx - 自定义错误边界
'use client';

import React from 'react';

interface ErrorBoundaryProps {
  children: React.ReactNode;
  fallback?: React.ReactNode;
}

interface ErrorBoundaryState {
  hasError: boolean;
  error?: Error;
}

export class ErrorBoundary extends React.Component<
  ErrorBoundaryProps,
  ErrorBoundaryState
> {
  constructor(props: ErrorBoundaryProps) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error: Error): ErrorBoundaryState {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    console.error('ErrorBoundary caught:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || (
        <div>
          <h2>Something went wrong.</h2>
          <button onClick={() => this.setState({ hasError: false })}>
            Try again
          </button>
        </div>
      );
    }

    return this.props.children;
  }
}
```

**练习项目：** 创建一个健壮的应用，包含完整的错误处理

---

### Day 21: Metadata与SEO优化
**知识点：**
- 静态Metadata
- 动态Metadata
- OpenGraph与Twitter Cards
- JSON-LD结构化数据

**代码示例：**
```typescript
// app/layout.tsx - 静态metadata
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: {
    default: 'My App',
    template: '%s | My App'
  },
  description: 'This is my awesome app',
  keywords: ['Next.js', 'React', 'TypeScript'],
  authors: [{ name: 'Your Name' }],
  creator: 'Your Name',
  openGraph: {
    type: 'website',
    locale: 'en_US',
    url: 'https://myapp.com',
    siteName: 'My App',
    images: [
      {
        url: 'https://myapp.com/og-image.jpg',
        width: 1200,
        height: 630,
        alt: 'My App'
      }
    ]
  },
  twitter: {
    card: 'summary_large_image',
    site: '@myapp',
    creator: '@yourname'
  },
  robots: {
    index: true,
    follow: true
  }
};

// app/blog/[slug]/page.tsx - 动态metadata
interface PageProps {
  params: { slug: string };
}

async function getPost(slug: string) {
  const res = await fetch(`https://api.example.com/posts/${slug}`);
  return res.json();
}

export async function generateMetadata(
  { params }: PageProps
): Promise<Metadata> {
  const post = await getPost(params.slug);

  return {
    title: post.title,
    description: post.excerpt,
    openGraph: {
      title: post.title,
      description: post.excerpt,
      type: 'article',
      publishedTime: post.publishedAt,
      authors: [post.author.name],
      images: [
        {
          url: post.coverImage,
          width: 1200,
          height: 630
        }
      ]
    }
  };
}

export default async function BlogPost({ params }: PageProps) {
  const post = await getPost(params.slug);

  return (
    <article>
      <h1>{post.title}</h1>
      <div dangerouslySetInnerHTML={{ __html: post.content }} />
    </article>
  );
}

// 生成sitemap - app/sitemap.ts
import { MetadataRoute } from 'next';

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
  const posts = await fetch('https://api.example.com/posts').then(res => 
    res.json()
  );

  const postEntries: MetadataRoute.Sitemap = posts.map((post: any) => ({
    url: `https://myapp.com/blog/${post.slug}`,
    lastModified: post.updatedAt,
    changeFrequency: 'weekly',
    priority: 0.8
  }));

  return [
    {
      url: 'https://myapp.com',
      lastModified: new Date(),
      changeFrequency: 'yearly',
      priority: 1
    },
    {
      url: 'https://myapp.com/about',
      lastModified: new Date(),
      changeFrequency: 'monthly',
      priority: 0.8
    },
    ...postEntries
  ];
}

// 生成robots.txt - app/robots.ts
import { MetadataRoute } from 'next';

export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow: '/',
      disallow: ['/admin/', '/api/']
    },
    sitemap: 'https://myapp.com/sitemap.xml'
  };
}

// JSON-LD结构化数据
export default function BlogPost({ post }: { post: any }) {
  const jsonLd = {
    '@context': 'https://schema.org',
    '@type': 'Article',
    headline: post.title,
    image: post.coverImage,
    datePublished: post.publishedAt,
    dateModified: post.updatedAt,
    author: {
      '@type': 'Person',
      name: post.author.name
    }
  };

  return (
    <>
      <script
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
      <article>{/* content */}</article>
    </>
  );
}
```

**练习项目：** 优化一个博客网站的SEO

---

### Day 22: API Routes与Route Handlers
**知识点：**
- Route Handlers
- Request与Response对象
- 中间件模式
- CORS配置

**代码示例：**
```typescript
// app/api/hello/route.ts - 基础GET请求
import { NextResponse } from 'next/server';

export async function GET() {
  return NextResponse.json({ message: 'Hello World' });
}

// app/api/users/route.ts - CRUD操作
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  const searchParams = request.nextUrl.searchParams;
  const page = searchParams.get('page') || '1';
  
  // 从数据库获取用户
  const users = await fetchUsers(parseInt(page));
  
  return NextResponse.json({ users, page });
}

export async function POST(request: NextRequest) {
  try {
    const body = await request.json();
    
    // 验证数据
    if (!body.name || !body.email) {
      return NextResponse.json(
        { error: 'Name and email are required' },
        { status: 400 }
      );
    }
    
    // 创建用户
    const user = await createUser(body);
    
    return NextResponse.json(user, { status: 201 });
  } catch (error) {
    return NextResponse.json(
      { error: 'Internal Server Error' },
      { status: 500 }
    );
  }
}

// app/api/users/[id]/route.ts - 动态路由
export async function GET(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await getUserById(params.id);
  
  if (!user) {
    return NextResponse.json(
      { error: 'User not found' },
      { status: 404 }
    );
  }
  
  return NextResponse.json(user);
}

export async function PUT(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const body = await request.json();
  const user = await updateUser(params.id, body);
  
  return NextResponse.json(user);
}

export async function DELETE(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  await deleteUser(params.id);
  
  return NextResponse.json({ success: true }, { status: 204 });
}

// lib/api-middleware.ts - 中间件模式
import { NextRequest, NextResponse } from 'next/server';

export type ApiHandler = (
  request: NextRequest,
  context?: any
) => Promise<NextResponse>;

export function withAuth(handler: ApiHandler): ApiHandler {
  return async (request: NextRequest, context?: any) => {
    const token = request.headers.get('authorization');
    
    if (!token) {
      return NextResponse.json(
        { error: 'Unauthorized' },
        { status: 401 }
      );
    }
    
    // 验证token
    const user = await verifyToken(token);
    
    if (!user) {
      return NextResponse.json(
        { error: 'Invalid token' },
        { status: 401 }
      );
    }
    
    // 将user添加到请求中
    return handler(request, { ...context, user });
  };
}

export function withCors(handler: ApiHandler): ApiHandler {
  return async (request: NextRequest, context?: any) => {
    const response = await handler(request, context);
    
    response.headers.set('Access-Control-Allow-Origin', '*');
    response.headers.set('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
    response.headers.set('Access-Control-Allow-Headers', 'Content-Type, Authorization');
    
    return response;
  };
}

// 使用中间件
// app/api/protected/route.ts
import { withAuth, withCors } from '@/lib/api-middleware';

async function handler(
  request: NextRequest,
  { user }: { user: any }
) {
  return NextResponse.json({ 
    message: 'Protected data',
    user 
  });
}

export const GET = withCors(withAuth(handler));

// app/api/upload/route.ts - 文件上传
export async function POST(request: NextRequest) {
  const formData = await request.formData();
  const file = formData.get('file') as File;
  
  if (!file) {
    return NextResponse.json(
      { error: 'No file uploaded' },
      { status: 400 }
    );
  }
  
  const bytes = await file.arrayBuffer();
  const buffer = Buffer.from(bytes);
  
  // 保存文件
  const path = await saveFile(buffer, file.name);
  
  return NextResponse.json({ path });
}
```

**练习项目：** 创建一个完整的RESTful API

---

### Day 23: Server Actions
**知识点：**
- Server Actions基础
- 表单处理
- Revalidation
- 错误处理

**代码示例：**
```typescript
// app/actions/user.ts
'use server';

import { revalidatePath } from 'next/cache';
import { redirect } from 'next/navigation';

export async function createUser(formData: FormData) {
  const name = formData.get('name') as string;
  const email = formData.get('email') as string;
  
  // 验证
  if (!name || !email) {
    return { error: 'Name and email are required' };
  }
  
  try {
    // 创建用户
    const user = await db.user.create({
      data: { name, email }
    });
    
    // 重新验证缓存
    revalidatePath('/users');
    
    return { success: true, user };
  } catch (error) {
    return { error: 'Failed to create user' };
  }
}

export async function deleteUser(userId: string) {
  await db.user.delete({
    where: { id: userId }
  });
  
  revalidatePath('/users');
  redirect('/users');
}

export async function updateUser(
  userId: string,
  formData: FormData
) {
  const name = formData.get('name') as string;
  
  const user = await db.user.update({
    where: { id: userId },
    data: { name }
  });
  
  revalidatePath(`/users/${userId}`);
  
  return user;
}

// components/CreateUserForm.tsx
'use client';

import { createUser } from '@/app/actions/user';
import { useFormState, useFormStatus } from 'react-dom';

function SubmitButton() {
  const { pending } = useFormStatus();
  
  return (
    <button
      type="submit"
      disabled={pending}
      className="px-4 py-2 bg-blue-500 text-white rounded disabled:opacity-50"
    >
      {pending ? 'Creating...' : 'Create User'}
    </button>
  );
}

export default function CreateUserForm() {
  const [state, formAction] = useFormState(createUser, null);

  return (
    <form action={formAction} className="space-y-4">
      <div>
        <label htmlFor="name">Name:</label>
        <input
          type="text"
          id="name"
          name="name"
          required
          className="block w-full p-2 border rounded"
        />
      </div>
      
      <div>
        <label htmlFor="email">Email:</label>
        <input
          type="email"
          id="email"
          name="email"
          required
          className="block w-full p-2 border rounded"
        />
      </div>
      
      {state?.error && (
        <p className="text-red-500">{state.error}</p>
      )}
      
      {state?.success && (
        <p className="text-green-500">User created successfully!</p>
      )}
      
      <SubmitButton />
    </form>
  );
}

// app/users/page.tsx - 使用Server Actions
import { deleteUser } from '@/app/actions/user';
import CreateUserForm from '@/components/CreateUserForm';

async function getUsers() {
  const users = await db.user.findMany();
  return users;
}

export default async function UsersPage() {
  const users = await getUsers();

  return (
    <div className="p-8">
      <h1 className="text-2xl font-bold mb-4">Users</h1>
      
      <CreateUserForm />
      
      <ul className="mt-8 space-y-2">
        {users.map((user) => (
          <li key={user.id} className="flex items-center justify-between p-4 border rounded">
            <div>
              <p className="font-semibold">{user.name}</p>
              <p className="text-gray-600">{user.email}</p>
            </div>
            <form action={deleteUser.bind(null, user.id)}>
              <button
                type="submit"
                className="px-3 py-1 bg-red-500 text-white rounded"
              >
                Delete
              </button>
            </form>
          </li>
        ))}
      </ul>
    </div>
  );
}

// 带验证的Server Action
import { z } from 'zod';

const userSchema = z.object({
  name: z.string().min(2).max(50),
  email: z.string().email(),
  age: z.number().min(18).max(120)
});

export async function createValidatedUser(formData: FormData) {
  const rawData = {
    name: formData.get('name'),
    email: formData.get('email'),
    age: parseInt(formData.get('age') as string)
  };
  
  const result = userSchema.safeParse(rawData);
  
  if (!result.success) {
    return { 
      error: 'Validation failed',
      fields: result.error.flatten().fieldErrors
    };
  }
  
  const user = await db.user.create({
    data: result.data
  });
  
  revalidatePath('/users');
  
  return { success: true, user };
}
```

**练习项目：** 创建一个待办事项应用，使用Server Actions

---

### Day 24: 中间件(Middleware)
**知识点：**
- Middleware基础
- 路由保护
- 重定向与重写
- Cookie操作

**代码示例：**
```typescript
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // 检查认证
  const token = request.cookies.get('token')?.value;
  
  if (!token && request.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  
  // 添加自定义header
  const response = NextResponse.next();
  response.headers.set('x-custom-header', 'my-value');
  
  return response;
}

export const config = {
  matcher: ['/dashboard/:path*', '/api/:path*']
};

// middleware.ts - 高级示例
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

// 验证JWT token
async function verifyAuth(token: string): Promise<boolean> {
  try {
    // 这里应该验证JWT
    return true;
  } catch {
    return false;
  }
}

export async function middleware(request: NextRequest) {
  const { pathname } = request.nextUrl;
  
  // 公共路径，不需要认证
  const publicPaths = ['/', '/login', '/register', '/api/auth'];
  if (publicPaths.some(path => pathname.startsWith(path))) {
    return NextResponse.next();
  }
  
  // 检查认证token
  const token = request.cookies.get('auth-token')?.value;
  
  if (!token) {
    const url = new URL('/login', request.url);
    url.searchParams.set('from', pathname);
    return NextResponse.redirect(url);
  }
  
  // 验证token
  const isValid = await verifyAuth(token);
  
  if (!isValid) {
    const response = NextResponse.redirect(new URL('/login', request.url));
    response.cookies.delete('auth-token');
    return response;
  }
  
  // 基于角色的访问控制
  if (pathname.startsWith('/admin')) {
    const userRole = request.cookies.get('user-role')?.value;
    
    if (userRole !== 'admin') {
      return NextResponse.redirect(new URL('/unauthorized', request.url));
    }
  }
  
  // 添加用户信息到headers
  const response = NextResponse.next();
  response.headers.set('x-user-token', token);
  
  return response;
}

export const config = {
  matcher: [
    '/((?!_next/static|_next/image|favicon.ico).*)',
  ]
};

// lib/middleware-utils.ts - 中间件工具
import { NextRequest, NextResponse } from 'next/server';

export function withLogging(
  handler: (request: NextRequest) => Promise<NextResponse>
) {
  return async (request: NextRequest) => {
    const start = Date.now();
    const response = await handler(request);
    const duration = Date.now() - start;
    
    console.log({
      method: request.method,
      path: request.nextUrl.pathname,
      status: response.status,
      duration: `${duration}ms`
    });
    
    return response;
  };
}

export function withRateLimit(
  handler: (request: NextRequest) => Promise<NextResponse>,
  limit: number = 100
) {
  const requests = new Map<string, number[]>();
  
  return async (request: NextRequest) => {
    const ip = request.ip || 'unknown';
    const now = Date.now();
    const windowMs = 60000; // 1分钟
    
    const userRequests = requests.get(ip) || [];
    const recentRequests = userRequests.filter(time => now - time < windowMs);
    
    if (recentRequests.length >= limit) {
      return new NextResponse('Too Many Requests', { status: 429 });
    }
    
    recentRequests.push(now);
    requests.set(ip, recentRequests);
    
    return handler(request);
  };
}

// 使用工具函数
export const middleware = withLogging(
  withRateLimit(async (request: NextRequest) => {
    // 你的中间件逻辑
    return NextResponse.next();
  })
);
```

**练习项目：** 创建一个包含认证和授权的应用

---

### Day 25: 图片优化(next/image)
**知识点：**
- Image组件
- 图片优化配置
- 响应式图片
- 模糊占位符

**代码示例：**
```typescript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  images: {
    domains: ['example.com', 'cdn.example.com'],
    remotePatterns: [
      {
        protocol: 'https',
        hostname: '**.unsplash.com',
      },
    ],
    formats: ['image/webp', 'image/avif'],
    deviceSizes: [640, 750, 828, 1080, 1200, 1920, 2048, 3840],
    imageSizes: [16, 32, 48, 64, 96, 128, 256, 384],
    minimumCacheTTL: 60,
  },
};

module.exports = nextConfig;

// components/OptimizedImage.tsx
import Image from 'next/image';

export default function OptimizedImage() {
  return (
    <div>
      {/* 基础用法 */}
      <Image
        src="/images/hero.jpg"
        alt="Hero"
        width={800}
        height={600}
        priority // LCP图片使用priority
      />
      
      {/* 远程图片 */}
      <Image
        src="https://example.com/photo.jpg"
        alt="Remote"
        width={800}
        height={600}
        quality={90}
      />
      
      {/* 响应式图片 */}
      <Image
        src="/images/responsive.jpg"
        alt="Responsive"
        fill
        sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
        style={{ objectFit: 'cover' }}
      />
      
      {/* 模糊占位符 */}
      <Image
        src="/images/placeholder.jpg"
        alt="Blur"
        width={800}
        height={600}
        placeholder="blur"
        blurDataURL="data:image/jpeg;base64,/9j/4AAQSkZJRg..."
      />
    </div>
  );
}

// lib/get-base64.ts - 生成模糊占位符
import { getPlaiceholder } from 'plaiceholder';

export async function getBase64(imageUrl: string) {
  try {
    const res = await fetch(imageUrl);
    
    if (!res.ok) {
      throw new Error(`Failed to fetch image: ${res.status} ${res.statusText}`);
    }
    
    const buffer = await res.arrayBuffer();
    
    const { base64 } = await getPlaiceholder(Buffer.from(buffer));
    
    return base64;
  } catch (error) {
    console.error(error);
    return 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mNk+M9QDwADhgGAWjR9awAAAABJRU5ErkJggg==';
  }
}

// app/gallery/page.tsx - 图片画廊
import Image from 'next/image';
import { getBase64 } from '@/lib/get-base64';

interface Photo {
  id: number;
  url: string;
  title: string;
}

async function getPhotos(): Promise<Photo[]> {
  // 获取图片列表
  return [
    { id: 1, url: 'https://example.com/photo1.jpg', title: 'Photo 1' },
    { id: 2, url: 'https://example.com/photo2.jpg', title: 'Photo 2' },
  ];
}

export default async function GalleryPage() {
  const photos = await getPhotos();
  
  const photosWithBlur = await Promise.all(
    photos.map(async (photo) => ({
      ...photo,
      blurDataUrl: await getBase64(photo.url)
    }))
  );

  return (
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 p-8">
      {photosWithBlur.map((photo) => (
        <div key={photo.id} className="relative aspect-square">
          <Image
            src={photo.url}
            alt={photo.title}
            fill
            sizes="(max-width: 768px) 100vw, (max-width: 1200px) 50vw, 33vw"
            className="object-cover rounded-lg"
            placeholder="blur"
            blurDataURL={photo.blurDataUrl}
          />
        </div>
      ))}
    </div>
  );
}
```

**练习项目：** 创建一个图片画廊应用，支持懒加载和优化

---

### Day 26: 字体优化(next/font)
**知识点：**
- Google Fonts优化
- 自定义字体
- 变量字体
- 字体子集

**代码示例：**
```typescript
// app/layout.tsx - Google Fonts
import { Inter, Roboto_Mono, Playfair_Display } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-inter',
});

const robotoMono = Roboto_Mono({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-roboto-mono',
});

const playfair = Playfair_Display({
  subsets: ['latin'],
  weight: ['400', '700'],
  style: ['normal', 'italic'],
  variable: '--font-playfair',
});

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en" className={`${inter.variable} ${robotoMono.variable} ${playfair.variable}`}>
      <body className={inter.className}>{children}</body>
    </html>
  );
}

// tailwind.config.js - 使用字体变量
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx,mdx}',
    './components/**/*.{js,ts,jsx,tsx,mdx}',
    './app/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ['var(--font-inter)'],
        mono: ['var(--font-roboto-mono)'],
        serif: ['var(--font-playfair)'],
      },
    },
  },
  plugins: [],
};

// app/fonts.ts - 自定义本地字体
import localFont from 'next/font/local';

export const customFont = localFont({
  src: [
    {
      path: '../public/fonts/CustomFont-Regular.woff2',
      weight: '400',
      style: 'normal',
    },
    {
      path: '../public/fonts/CustomFont-Bold.woff2',
      weight: '700',
      style: 'normal',
    },
  ],
  variable: '--font-custom',
});

// 使用自定义字体
// app/page.tsx
import { customFont } from './fonts';

export default function Home() {
  return (
    <div className={customFont.className}>
      <h1>Custom Font Heading</h1>
    </div>
  );
}

// 条件字体加载
// components/DynamicFont.tsx
'use client';

import { Noto_Sans_SC } from 'next/font/google';
import { useState } from 'react';

const notoSansSC = Noto_Sans_SC({
  subsets: ['latin'],
  weight: ['400', '700'],
});

export default function DynamicFont() {
  const [isChineseFont, setIsChineseFont] = useState(false);

  return (
    <div className={isChineseFont ? notoSansSC.className : ''}>
      <button onClick={() => setIsChineseFont(!isChineseFont)}>
        Toggle Chinese Font
      </button>
      <p>这是中文文本 / This is English text</p>
    </div>
  );
}
```

**练习项目：** 创建一个多语言网站，优化字体加载

---

### Day 27: 国际化(i18n)
**知识点：**
- 多语言路由
- 翻译文件管理
- 语言切换
- 动态内容翻译

**代码示例：**
```typescript
// i18n.config.ts
export const i18n = {
  defaultLocale: 'en',
  locales: ['en', 'zh', 'es', 'fr'],
} as const;

export type Locale = (typeof i18n)['locales'][number];

// middleware.ts - 语言检测和重定向
import { NextRequest, NextResponse } from 'next/server';
import { i18n } from './i18n.config';

function getLocale(request: NextRequest): string {
  const pathname = request.nextUrl.pathname;
  const pathnameLocale = i18n.locales.find(
    (locale) => pathname.startsWith(`/${locale}/`) || pathname === `/${locale}`
  );

  if (pathnameLocale) return pathnameLocale;

  // 从Accept-Language header检测
  const acceptLanguage = request.headers.get('accept-language');
  if (acceptLanguage) {
    const preferredLocale = acceptLanguage
      .split(',')[0]
      .split('-')[0];
    
    if (i18n.locales.includes(preferredLocale as any)) {
      return preferredLocale;
    }
  }

  return i18n.defaultLocale;
}

export function middleware(request: NextRequest) {
  const pathname = request.nextUrl.pathname;
  
  const pathnameIsMissingLocale = i18n.locales.every(
    (locale) => !pathname.startsWith(`/${locale}/`) && pathname !== `/${locale}`
  );

  if (pathnameIsMissingLocale) {
    const locale = getLocale(request);
    return NextResponse.redirect(
      new URL(`/${locale}${pathname}`, request.url)
    );
  }
}

export const config = {
  matcher: ['/((?!api|_next/static|_next/image|favicon.ico).*)'],
};

// dictionaries/en.json
{
  "navigation": {
    "home": "Home",
    "about": "About",
    "contact": "Contact"
  },
  "home": {
    "title": "Welcome to our website",
    "description": "This is a multilingual Next.js application"
  },
  "common": {
    "language": "Language",
    "submit": "Submit",
    "cancel": "Cancel"
  }
}

// dictionaries/zh.json
{
  "navigation": {
    "home": "首页",
    "about": "关于",
    "contact": "联系"
  },
  "home": {
    "title": "欢迎来到我们的网站",
    "description": "这是一个多语言Next.js应用"
  },
  "common": {
    "language": "语言",
    "submit": "提交",
    "cancel": "取消"
  }
}

// lib/get-dictionary.ts
import 'server-only';
import type { Locale } from '@/i18n.config';

const dictionaries = {
  en: () => import('@/dictionaries/en.json').then((module) => module.default),
  zh: () => import('@/dictionaries/zh.json').then((module) => module.default),
  es: () => import('@/dictionaries/es.json').then((module) => module.default),
  fr: () => import('@/dictionaries/fr.json').then((module) => module.default),
};

export const getDictionary = async (locale: Locale) => {
  return dictionaries[locale]?.() ?? dictionaries.en();
};

// app/[lang]/layout.tsx
import { i18n, type Locale } from '@/i18n.config';
import LocaleSwitcher from '@/components/LocaleSwitcher';

export async function generateStaticParams() {
  return i18n.locales.map((locale) => ({ lang: locale }));
}

export default function LocaleLayout({
  children,
  params,
}: {
  children: React.ReactNode;
  params: { lang: Locale };
}) {
  return (
    <html lang={params.lang}>
      <body>
        <header>
          <LocaleSwitcher currentLocale={params.lang} />
        </header>
        {children}
      </body>
    </html>
  );
}

// app/[lang]/page.tsx
import { getDictionary } from '@/lib/get-dictionary';
import type { Locale } from '@/i18n.config';

export default async function HomePage({
  params: { lang },
}: {
  params: { lang: Locale };
}) {
  const dict = await getDictionary(lang);

  return (
    <div>
      <h1>{dict.home.title}</h1>
      <p>{dict.home.description}</p>
    </div>
  );
}

// components/LocaleSwitcher.tsx
'use client';

import Link from 'next/link';
import { usePathname } from 'next/navigation';
import { i18n, type Locale } from '@/i18n.config';

export default function LocaleSwitcher({
  currentLocale,
}: {
  currentLocale: Locale;
}) {
  const pathname = usePathname();

  const redirectedPathname = (locale: Locale) => {
    if (!pathname) return '/';
    const segments = pathname.split('/');
    segments[1] = locale;
    return segments.join('/');
  };

  return (
    <div className="flex gap-2">
      {i18n.locales.map((locale) => (
        <Link
          key={locale}
          href={redirectedPathname(locale)}
          className={locale === currentLocale ? 'font-bold' : ''}
        >
          {locale.toUpperCase()}
        </Link>
      ))}
    </div>
  );
}
```

**练习项目：** 创建一个多语言电商网站

---

### Day 28: 性能优化
**知识点：**
- 代码分割
- 懒加载
- Bundle分析
- 性能监控

**代码示例：**
```typescript
// 动态导入 - 组件懒加载
import dynamic from 'next/dynamic';

const DynamicComponent = dynamic(() => import('@/components/HeavyComponent'), {
  loading: () => <p>Loading...</p>,
  ssr: false, // 禁用SSR
});

const DynamicComponentWithOptions = dynamic(
  () => import('@/components/Chart'),
  {
    loading: () => <div>Loading chart...</div>,
    ssr: false,
  }
);

export default function Page() {
  return (
    <div>
      <DynamicComponent />
      <DynamicComponentWithOptions />
    </div>
  );
}

// 条件加载
'use client';

import { useState } from 'react';
import dynamic from 'next/dynamic';

const AdminPanel = dynamic(() => import('@/components/AdminPanel'));

export default function Dashboard() {
  const [showAdmin, setShowAdmin] = useState(false);

  return (
    <div>
      <button onClick={() => setShowAdmin(true)}>
        Show Admin Panel
      </button>
      {showAdmin && <AdminPanel />}
    </div>
  );
}

// 命名导出的动态导入
const DynamicHeader = dynamic(
  () => import('@/components/Layout').then((mod) => mod.Header)
);

// lib/performance.ts - 性能监控
export function reportWebVitals(metric: any) {
  console.log(metric);
  
  // 发送到分析服务
  if (metric.label === 'web-vital') {
    // 例如: Google Analytics
    window.gtag?.('event', metric.name, {
      value: Math.round(metric.value),
      event_label: metric.id,
      non_interaction: true,
    });
  }
}

// app/layout.tsx
import { Suspense } from 'react';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html>
      <body>
        <Suspense fallback={<div>Loading...</div>}>
          {children}
        </Suspense>
      </body>
    </html>
  );
}

// next.config.js - Bundle分析
const withBundleAnalyzer = require('@next/bundle-analyzer')({
  enabled: process.env.ANALYZE === 'true',
});

/** @type {import('next').NextConfig} */
const nextConfig = {
  // 编译优化
  swcMinify: true,
  
  // 压缩配置
  compress: true,
  
  // 实验性特性
  experimental: {
    optimizeCss: true,
    optimizePackageImports: ['lodash', 'date-fns'],
  },
  
  // Webpack配置
  webpack: (config, { dev, isServer }) => {
    // 生产环境优化
    if (!dev && !isServer) {
      config.optimization.splitChunks = {
        chunks: 'all',
        cacheGroups: {
          default: false,
          vendors: false,
          commons: {
            name: 'commons',
            chunks: 'all',
            minChunks: 2,
          },
          lib: {
            test: /[\\/]node_modules[\\/]/,
            name: (module) => {
              const packageName = module.context.match(
                /[\\/]node_modules[\\/](.*?)([\\/]|$)/
              )[1];
              return `npm.${packageName.replace('@', '')}`;
            },
          },
        },
      };
    }
    
    return config;
  },
};

module.exports = withBundleAnalyzer(nextConfig);

// components/LazyImage.tsx - 图片懒加载
'use client';

import { useState, useEffect, useRef } from 'react';
import Image from 'next/image';

interface LazyImageProps {
  src: string;
  alt: string;
  width: number;
  height: number;
}

export default function LazyImage({ src, alt, width, height }: LazyImageProps) {
  const [isVisible, setIsVisible] = useState(false);
  const imgRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setIsVisible(true);
          observer.disconnect();
        }
      },
      { threshold: 0.1 }
    );

    if (imgRef.current) {
      observer.observe(imgRef.current);
    }

    return () => observer.disconnect();
  }, []);

  return (
    <div ref={imgRef}>
      {isVisible ? (
        <Image src={src} alt={alt} width={width} height={height} />
      ) : (
        <div style={{ width, height, backgroundColor: '#f0f0f0' }} />
      )}
    </div>
  );
}

// 使用React.memo优化重渲染
import { memo } from 'react';

interface UserCardProps {
  user: {
    id: number;
    name: string;
    email: string;
  };
}

const UserCard = memo(function UserCard({ user }: UserCardProps) {
  return (
    <div>
      <h3>{user.name}</h3>
      <p>{user.email}</p>
    </div>
  );
});

export default UserCard;
```

**练习项目：** 优化一个现有应用的性能指标

---

### Day 29: 认证与授权
**知识点：**
- NextAuth.js集成
- JWT与Session
- OAuth providers
- 路由保护

**代码示例：**
```typescript
// 安装依赖
// npm install next-auth @auth/prisma-adapter

// lib/auth.ts
import { NextAuthOptions } from 'next-auth';
import CredentialsProvider from 'next-auth/providers/credentials';
import GoogleProvider from 'next-auth/providers/google';
import GitHubProvider from 'next-auth/providers/github';
import { PrismaAdapter } from '@auth/prisma-adapter';
import { prisma } from './prisma';
import bcrypt from 'bcryptjs';

export const authOptions: NextAuthOptions = {
  adapter: PrismaAdapter(prisma),
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID!,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET!,
    }),
    GitHubProvider({
      clientId: process.env.GITHUB_ID!,
      clientSecret: process.env.GITHUB_SECRET!,
    }),
    CredentialsProvider({
      name: 'Credentials',
      credentials: {
        email: { label: 'Email', type: 'email' },
        password: { label: 'Password', type: 'password' },
      },
      async authorize(credentials) {
        if (!credentials?.email || !credentials?.password) {
          throw new Error('Invalid credentials');
        }

        const user = await prisma.user.findUnique({
          where: { email: credentials.email },
        });

        if (!user || !user.hashedPassword) {
          throw new Error('Invalid credentials');
        }

        const isValid = await bcrypt.compare(
          credentials.password,
          user.hashedPassword
        );

        if (!isValid) {
          throw new Error('Invalid credentials');
        }

        return {
          id: user.id,
          email: user.email,
          name: user.name,
          role: user.role,
        };
      },
    }),
  ],
  session: {
    strategy: 'jwt',
  },
  callbacks: {
    async jwt({ token, user }) {
      if (user) {
        token.role = user.role;
      }
      return token;
    },
    async session({ session, token }) {
      if (session.user) {
        session.user.role = token.role;
      }
      return session;
    },
  },
  pages: {
    signIn: '/login',
    error: '/auth/error',
  },
};

// app/api/auth/[...nextauth]/route.ts
import NextAuth from 'next-auth';
import { authOptions } from '@/lib/auth';

const handler = NextAuth(authOptions);

export { handler as GET, handler as POST };

// app/login/page.tsx
'use client';

import { signIn } from 'next-auth/react';
import { useState } from 'react';
import { useRouter } from 'next/navigation';

export default function LoginPage() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');
  const router = useRouter();

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setError('');

    try {
      const result = await signIn('credentials', {
        email,
        password,
        redirect: false,
      });

      if (result?.error) {
        setError('Invalid credentials');
        return;
      }

      router.push('/dashboard');
    } catch (error) {
      setError('Something went wrong');
    }
  };

  const handleOAuthSignIn = (provider: string) => {
    signIn(provider, { callbackUrl: '/dashboard' });
  };

  return (
    <div className="flex min-h-screen items-center justify-center">
      <div className="w-full max-w-md space-y-8 p-8">
        <h2 className="text-3xl font-bold text-center">Sign In</h2>
        
        {error && (
          <div className="bg-red-100 text-red-700 p-3 rounded">
            {error}
          </div>
        )}

        <form onSubmit={handleSubmit} className="space-y-4">
          <div>
            <label htmlFor="email">Email</label>
            <input
              id="email"
              type="email"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
              className="w-full p-2 border rounded"
              required
            />
          </div>

          <div>
            <label htmlFor="password">Password</label>
            <input
              id="password"
              type="password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              className="w-full p-2 border rounded"
              required
            />
          </div>

          <button
            type="submit"
            className="w-full bg-blue-500 text-white p-2 rounded"
          >
            Sign In
          </button>
        </form>

        <div className="space-y-2">
          <button
            onClick={() => handleOAuthSignIn('google')}
            className="w-full bg-red-500 text-white p-2 rounded"
          >
            Sign in with Google
          </button>
          
          <button
            onClick={() => handleOAuthSignIn('github')}
            className="w-full bg-gray-800 text-white p-2 rounded"
          >
            Sign in with GitHub
          </button>
        </div>
      </div>
    </div>
  );
}

// components/SessionProvider.tsx
'use client';

import { SessionProvider as Provider } from 'next-auth/react';

export default function SessionProvider({
  children,
}: {
  children: React.ReactNode;
}) {
  return <Provider>{children}</Provider>;
}

// app/layout.tsx
import SessionProvider from '@/components/SessionProvider';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html>
      <body>
        <SessionProvider>{children}</SessionProvider>
      </body>
    </html>
  );
}

// components/UserButton.tsx
'use client';

import { useSession, signOut } from 'next-auth/react';

export default function UserButton() {
  const { data: session, status } = useSession();

  if (status === 'loading') {
    return <div>Loading...</div>;
  }

  if (!session) {
    return null;
  }

  return (
    <div className="flex items-center gap-4">
      <span>Welcome, {session.user?.name}</span>
      <button
        onClick={() => signOut()}
        className="px-4 py-2 bg-red-500 text-white rounded"
      >
        Sign Out
      </button>
    </div>
  );
}

// middleware.ts - 路由保护
import { withAuth } from 'next-auth/middleware';
import { NextResponse } from 'next/server';

export default withAuth(
  function middleware(req) {
    // 检查用户角色
    if (
      req.nextUrl.pathname.startsWith('/admin') &&
      req.nextauth.token?.role !== 'admin'
    ) {
      return NextResponse.redirect(new URL('/unauthorized', req.url));
    }
  },
  {
    callbacks: {
      authorized: ({ token }) => !!token,
    },
  }
);

export const config = {
  matcher: ['/dashboard/:path*', '/admin/:path*'],
};
```

**练习项目：** 创建一个完整的用户认证系统

---

### Day 30: 数据库集成(Prisma)
**知识点：**
- Prisma设置
- 数据模型定义
- CRUD操作
- 关系查询

**代码示例：**
```typescript
// 安装依赖
// npm install prisma @prisma/client
// npx prisma init

// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id            String    @id @default(cuid())
  name          String?
  email         String    @unique
  emailVerified DateTime?
  image         String?
  hashedPassword String?
  role          String    @default("user")
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
  
  posts         Post[]
  comments      Comment[]
  accounts      Account[]
  sessions      Session[]
}

model Account {
  id                String  @id @default(cuid())
  userId            String
  type              String
  provider          String
  providerAccountId String
  refresh_token     String?
  access_token      String?
  expires_at        Int?
  token_type        String?
  scope             String?
  id_token          String?
  session_state     String?

  user User @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@unique([provider, providerAccountId])
}

model Session {
  id           String   @id @default(cuid())
  sessionToken String   @unique
  userId       String
  expires      DateTime
  user         User     @relation(fields: [userId], references: [id], onDelete: Cascade)
}

model Post {
  id        String    @id @default(cuid())
  title     String
  content   String?
  published Boolean   @default(false)
  createdAt DateTime  @default(now())
  updatedAt DateTime  @updatedAt
  authorId  String
  
  author    User      @relation(fields: [authorId], references: [id])
  comments  Comment[]
  
  @@index([authorId])
}

model Comment {
  id        String   @id @default(cuid())
  content   String
  createdAt DateTime @default(now())
  postId    String
  authorId  String
  
  post      Post     @relation(fields: [postId], references: [id], onDelete: Cascade)
  author    User     @relation(fields: [authorId], references: [id])
  
  @@index([postId])
  @@index([authorId])
}

// lib/prisma.ts
import { PrismaClient } from '@prisma/client';

const globalForPrisma = globalThis as unknown as {
  prisma: PrismaClient | undefined;
};

export const prisma =
  globalForPrisma.prisma ??
  new PrismaClient({
    log: ['query', 'error', 'warn'],
  });

if (process.env.NODE_ENV !== 'production') {
  globalForPrisma.prisma = prisma;
}

// lib/db/users.ts
import { prisma } from '@/lib/prisma';
import bcrypt from 'bcryptjs';

export async function createUser(data: {
  email: string;
  name: string;
  password: string;
}) {
  const hashedPassword = await bcrypt.hash(data.password, 10);
  
  return prisma.user.create({
    data: {
      email: data.email,
      name: data.name,
      hashedPassword,
    },
  });
}

export async function getUserByEmail(email: string) {
  return prisma.user.findUnique({
    where: { email },
    include: {
      posts: true,
    },
  });
}

export async function updateUser(id: string, data: { name?: string; email?: string }) {
  return prisma.user.update({
    where: { id },
    data,
  });
}

export async function deleteUser(id: string) {
  return prisma.user.delete({
    where: { id },
  });
}

// lib/db/posts.ts
export async function getPosts(params?: {
  page?: number;
  pageSize?: number;
  published?: boolean;
}) {
  const { page = 1, pageSize = 10, published } = params || {};
  
  const where = published !== undefined ? { published } : {};
  
  const [posts, total] = await Promise.all([
    prisma.post.findMany({
      where,
      include: {
        author: {
          select: {
            name: true,
            email: true,
          },
        },
        _count: {
          select: {
            comments: true,
          },
        },
      },
      orderBy: {
        createdAt: 'desc',
      },
      skip: (page - 1) * pageSize,
      take: pageSize,
    }),
    prisma.post.count({ where }),
  ]);
  
  return {
    posts,
    pagination: {
      page,
      pageSize,
      total,
      totalPages: Math.ceil(total / pageSize),
    },
  };
}

export async function getPostById(id: string) {
  return prisma.post.findUnique({
    where: { id },
    include: {
      author: true,
      comments: {
        include: {
          author: {
            select: {
              name: true,
              image: true,
            },
          },
        },
        orderBy: {
          createdAt: 'desc',
        },
      },
    },
  });
}

export async function createPost(data: {
  title: string;
  content: string;
  authorId: string;
  published?: boolean;
}) {
  return prisma.post.create({
    data,
  });
}

// app/api/posts/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { getPosts, createPost } from '@/lib/db/posts';
import { getServerSession } from 'next-auth';
import { authOptions } from '@/lib/