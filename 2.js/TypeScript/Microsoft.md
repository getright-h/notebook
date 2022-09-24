# TypeScript 

## 1. 基础

### 1.1 安装 TypeScript

TypeScript 在 npm 注册表中以 typescript 包的形式提供。 安装最新版本的 TypeScript：

1. 在“命令提示符”窗口中，输入 `npm install -g typescript`。
2. 输入 `tsc` 确认已安装 TypeScript。 如果已成功安装，则此命令应显示编译器命令和选项列表。



### 1.2 编译 TypeScript 文件

在命令提示符下使用 `tsc` 命令运行 TypeScript 编译器。 在不使用其他参数的情况下运行 `tsc` 时，它将编译当前文件夹中的所有 .ts 文件，并为每个文件生成一个 .js 文件。

你也可以编译特定的文件。 例如，若要编译名为 utility_functions.ts 的 TypeScript 文件，请输入 `tsc utility_functions.ts`。





### 1.3 编译器选项

使用编译器选项，可以控制如何从源 TypeScript 生成 JavaScript。 你可在命令提示符处（就像在许多命令行界面中一样）设置选项，也可以在名为 tsconfig.json 的 JSON 文件中设置选项。

有许多编译器选项可供选择。 在 [tsc 命令行接口文档](https://www.typescriptlang.org/docs/handbook/compiler-options.html)中可以找到选项的完整列表。 以下介绍了一些最常见的方式：

- `noImplicitAny`
- `noEmitOnError`
- `target`
- 目录选项

若要控制编译，可以将编译器选项与 `tsc` 命令一起使用，包括：

- `--noImplicitAny` 选项，指示编译器对具有隐含的 `any` 类型的表达式和声明引发错误。 例如：

  `tsc utility_functions.ts --noImplicitAny`

- `--target` 选项，为 JavaScript 文件指定 ECMAScript 目标版本。 此示例编译与 ECMAScript 6 兼容的 JavaScript 文件：

  `tsc utility_functions.ts --target "ES2015"`



### 1.生成 tsconfig.json 文件

在编译 TypeScript 源代码时，TypeScript 编译器会应用默认行为。 但你可以通过将 tsconfig.json 文件添加到 TypeScript 项目文件夹的根目录来修改 TypeScript 编译器选项。 此文件定义了 TypeScript 项目设置，例如编译器选项和应包括的文件。

你可以使用 TypeScript 编译器的 `init` 选项，生成具有默认选项的 tsconfig.json 文件。

1. 在 Visual Studio Code 中，选择“终端”>“新建终端”，打开新的终端窗口。

2. 在命令提示符处，输入 `tsc --init`。

   注意，新的 tsconfig.json 文件已添加到“资源管理器”窗格中。 可能需要刷新“资源管理器”窗格以查看文件。

3. 在代码编辑器中打开 tsconfig.json 文件。 你将看到它具有许多选项，其中大部分都被注释掉了。查看每个启用的选项的说明。

4. 在 tsconfig.json 文件中，查找目标选项，并将其更改为 `"ES2015"`。

5. 更新 tsconfig.json 文件，以便编译器将所有 JavaScript 文件保存到新文件夹中。

   a. 在“资源管理器”窗格中，在项目中创建一个名为“build”的新文件夹。
   b. 在 tsconfig.json 文件中，查找 `outDir` 选项，删除注释，并将参数设置为“build”。

6. 保存 tsconfig.json 文件。

7. 在命令提示符处，输入 `tsc`。 这会读取 tsconfig.json 文件并重置项目的选项。



## 2. 初探

```typescript

// 匹配多个任意类型属性
let c: { name: number, [propName: string]: any }
// ?表示属性可选
let b: { name: string, age?: number }
// unknown 在用的时候再声明类型
let u: unknown;
u = 10;
u = 'hello';
const a: string = u as string
// 元组 限定数组元素
let arr: [string[], object, string]
arr = [[], {}, '12']
// 枚举 定义一组带名字的常量 其中的属性不赋值的是数值类型(数值会从0自增) ，否则是字符串类型
enum Gender {
    male,
    female
}
// 和枚举的名字来访问枚举类型
let p: { name: string, gender: Gender }
// 通过枚举的属性来访问枚举成员，
p = { name: 'alex', gender: Gender.female }
// 或
let _a1: string | number
_a1 = 1
_a1 = '1'
// 与 一般用在对象
let _a2: { name: string } & { age: number }
_a2 = { name: 'alex', age: 1 }
// 接口 相当于自定义一个类型
interface _a3 {
    name: string,
    age: number,
    id?: string
}

function a3(): _a3 {
    let a3_1 = { name: 'alex', age: 1 }
    return a3_1
}
```

