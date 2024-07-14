# 普通类型

- i32 : 32位有符号整型
- u32 : 32位无符号整型
- f32 : 32位浮点型
- bool : boolean类型
- f16 : 16位浮点型(可选功能,需要主动开启)

# 变量声明

跟typescript一样,需要在每个变量或者函数体后面添加类型
```RUST
var a: f32 = 1;
let c: f32 = 3; //定义以后不能修改,常数
fn d(e: f32) -> f32 { return e * 2; }
```

# 自动类型(隐式声明)
```RUST
let a = 1;          // a is an i32
let b = 2.0;        // b is a f32
let c = f32(a) + b; // ok
```

```RUST
const one = 1;
const two = one *2;
const PI = radians(180.0);

fn add(a: f32, n: f32) -> f32 {
	const result = a + b; // ERROR!const can only be used with compile time expressions
	return result;
}
```

# 矢量Vector

- vec2
- vec3
- vec4

基本风格
`vec2<i32>`是一个包含2个i32数值的矢量，`vec3<f32>`是一个包含3个f32元素的矢量，`vec4<u32>`是一个包含4个u32数值的矢量，`vec3<bool>`一个包含3个布尔值的矢量。

```rust
let a = vec2<i32>(1,-2);
let b = vec3<f32>(3.4,5.6,7.8);
let c = vec4<u32>(9,10);
```

访问
```rust
let a = vec4<f32>(1, 2, 3, 4);
let b = a.z;    //代表着x,y,z,w
let c = a.b;    //代表着r,g,b,a
let d = a[2];   //代表数组元素访问

//也可以一次访问多个元素
let a = vec4<f32>(1, 2, 3, 4);
let b = a.zx;   // via x,y,z,w
let c = a.br;   // via r,g,b,a
let d = vec2<f32>(a[2], a[0]);

//重复取值
let a = vec4<f32>(1, 2, 3, 4);
let v = vec3<f32>(a.z, a.z, a.y);
let c = a.zzy;
```

# 简写

```rust
let a = vec4<f32>(1, 2, 3, 4);
let b = vec4f(1, 2, 3, 4);

let a = vec4f(1, 2, 3, 4);
let b = vec2f(2, 3);
let c = vec4f(1, b, 4);
let d = vec4f(1, a.yz, 4);
let e = vec4f(a.xyz, 4);
let f = vec4f(1, a.yzw);
```

# 数学运算

```rust
let a = vec4f(1, 2, 3, 4);
let b = vec4f(5, 6, 7, 8);
let c = a + b;  // c is vec4f(6, 8, 10, 12)
let d = a * b;
let e = a - b;
```

```rust
//函数直接使用
let a = vec4f(1, 2, 3, 4);
let b = vec4f(5, 6, 7, 8);
let c = mix(a, b, 0.5);                   // c is vec4f(3, 4, 5, 6)
let d = mix(a, b, vec4f(0, 0.5, 0.5, 1)); // d is vec4f(1, 4, 5, 8)

//mix函数(混入函数)
//mix(x, y, a)  x, y的线性混叠, x(1-a) + y*a; a为0 结果为x,a为1 结果为y 
//1 2   3   4
//5 6   7   8
//0 0.5 0.5 1
//1 4   5   8
```

```rust
let a = mat4x4f(...);
let b = a[2];

//3D场景中矩阵和矢量的运算  mat4x4f可以直接和vec4f相乘生成一个新的vec4f
let a = mat3x4f(....);
let b = vec4f(1, 2, 3, 4);
let c = a * b
```

# 数组arrays

```rust
let a = array<f32, 5>;
let b = array<vec4f, 6>;


//其他构造方式,它接受任意数组的参数并返回一个数组,而且参数必须是相同的类型
let arrOf3Vec3fsA = array(vec3f(1,2,3), vec3f(4,5,6), vec3f(7,8,9));
let arrOf3Vec3fsB = array<vec3f, 3>(vec3f(1,2,3), vec3f(4,5,6), vec3f(7,8,9));
```

# runtime side arrays
```rust
//位于根作用域的存储声明中的数组是唯一可以不指定大小的数组。
@group(0) @binding(0) var<storage> foo: array<mat4x4f>;
//`foo`中的元素数量由运行时使用的绑定组的设置定义，也可以在WGSL中使用`arrayLength`查询长度。
let numMatrices = arrayLength(&foo);
```

# 函数
```rust
fn add(a: f32, b: f32) -> f32{
	return a + b;
}
```

# 着色器入口 entry points
```rust
@vertex fn myFunc(a: f32, b: f32) -> @builtin(position): vecc4f{
	return vec4f(0, 0, 0, 0);
}
```

# 着色器只通过WGSL入口访问
```rust
@group(0) @bingding(0) var<uniforms> uni: vec4f;

vec4f fn foo(){
	return uni;
}

@vertex fn vs1(): @builtin(position) vec4f {
	return vec4f(0);
}

@vertex fn vs2(): @builtin(position) vec4f {
	return foo();
}
```

# 属性attributes
```rust
@location(number)

@location(number) 用来定义着色器的输入和输出
```

# 顶点着色器输入 vertex shader inputs

```rust
@vertex vs1(@location(0) foo: f32,@location(1) bar: vec4f)...

struct Stuff{
	@location(0) foo: f32,
	@location(1) bar: vec4f
}

@vertex vs2(s: Stuff) ...

//vs1和vs2都是在location(0) 和 location(1)上声明顶点着色器的输入,这些输入需要由顶点缓存去提供数据
```


# 阶段变量 inter stage variables
```rust
struct VSOut{
	@builtin(position) pos: vec4f,
	@location(0) color: vec4f;
	@location(1) texcoords: vec2f
};

struct FSIn{
	@location(1) uv: vec2f,
	@location(0) diffuse: vec4f
}

@vertex fn foo(...) -> VSOut { ... }
@fragment fn bar(moon: FSIn) ...
```

```rust
struct FSOut{
	@location(0) albedo: vec4f;
	@location(1) normal: vec4f;
}

@fragment fn bar(...) -> FSOut {...}
```

#### @builtin(name)

```rust
//@builtin(name)属性通常用于指定来之WebGPU内置变量的值
@vertex fn vs1(@builtin(vertex_index) foo: u32,@builtin(instance_index) bar:u32)...{
	...
}

// foo从内置特性vertex_index取值
// bar从内置特性instance_index取值
```

```rust
struct Foo {
	@builtin(vertex_index) vNdx: u32,
	@builtin(instance_index) iNdx: u32
}

@vertex fn vs1(blap: Foo)...{
	...
}
```

# if, while, switch, break-if 逻辑表达式不需要括号

```text
if a < 5 {
  doTheThing();
}
```

# 不支持三元运算符
```rust
//可以使用select
let a = select(falseExpression,trueExpression,condition);
```

# ++ 和 -- 是语句,不是表达式

```text
var a = 5;
a++;          // is now 6
++a;          // ERROR: no such thing has pre-increment
let b = a++;  // ERROR: a++ is not an expression, it's a statement
```

# += 和 -= 不是表达式,而是赋值语句

```js
let a = 5;
a += 2;          // a = 7
let b = a += 2;  // a = 9, b = 9
let a = 5;
a += 2;           // a is 7
let b = a += 2;  // ERROR: a += 2 is not an expression
```

# 不支持值交换

```text
var color = vec4f(0.25, 0.5, 0.75, 1);
color.rgb = color.bgr; // ERROR
color = vec4(color.bgr, 1);  // Ok
```

# 虚构赋值操作

```rust
@group(0) @binding(0) var<uniforms> uni1: vec4f;
@group(0) @binding(0) var<uniforms> uni2: mat4x4f;

@vertex fn vs1(): @builtin(position) vec4f{
	return vec4f(0);
}

@vertex fn vs2(): @builtin(position) vec4f{
	_ = uni1;
	_ = uni2;
	return vec4f(0);
}
```