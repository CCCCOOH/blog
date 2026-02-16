> 春节期间不知道干啥，游戏都删了也没带手柄回乡下，那就浅学一下一直想学的 `Ts` 吧！
## 类型相关

```typescript
// 根据初始值进行变量类型限定——自动推断
let str = 'abc'

// 主动类型注解——主动出击🚀
let str: string = 'abc'
let str: string
let v1: number
let v2: boolean
let v3: null = null
let v4: undefined = undefined

// 联合类型
let v5： string | null = null // 若使用配置项strictNullChecks就不能随意将null分配给其他类型
let v6: 1 | 2 | 3 = 2

// 数组
let arr: number[] = [1, 2, 3]
let arr1: Array<number> = ['a', 'b', 'c']

// 元组
let t1: [number, string, number?] = [1, 'a', 2]    // ?表示可选值，可以去掉
let t1: [number, string, number?] = [1, 'a']    //?可去
t1[0] = 'a' // 只能访问，赋值爆错

// 枚举
enum MyEnum {
    A,
    B,
    C
}
console.log(MyEnum.A)
console.log(MyEnum[0])

// 类型断言
let numArr = [1,2,3]
const res = numArr.find(item => item > 2) as number
res * 5

// 类型别名
type MyUserName = string | number
let a: MyUserName = 10
let b: MyUserName = 'abc'
```

## 函数

```typescript
// 函数
function MyFn1(a: number, b: string): Void {    // Void 表示没有返回值
    return a + b // 爆错
}
function MyFn(a = 10, b?: string, c?: boolean, ...rest: number[]): number {    // 可选参数（所有可选参数必须在尾部）
    return 100
}
const f = MyFn(20, 'abc', true, 1, 2, 3)
```


## 接口

一般用于对象的定义。

```c
interface Obj = {
    name: string,
    age: number
}

const obj: Obj = {
    name: 'Sy',
    age: 13
}
```

## 范型

通用的类型。

```typescript
function myFn(a: number, b: number): number[] {
    return [a, b]
} // 如果我不只是想传入number呢？🤔

// 通过范型优化后
function myFn<T>(a: T, b: T): T[] {
    return [a, b]
}

myFn<number>(1, 'a')    // 爆错，'a'不是<number>类型
myFn<string>('a', 'b')
myFn('a', 'b')          // 也可以省略<T>，Ts会根据行参进行非常“智能”的类型推断
```