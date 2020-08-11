# Eloquent JavaScript (chapter 0-2)

## Introduction

It is up to you to make the necessary effort. When you are struggling to follow the book, do not jump to any conclusions about your own capabilities. You are fine—you just need to keep at it. Take a break, reread some material, and make sure you read and understand the example programs and exercises. Learning is hard work, but everything you learn is yours and will make subsequent learning easier.

The art of programming is the skill of controlling complexity.

A sense of what a good program looks like is developed in practice, not learned from a list of rules.

## Values, Types, and Operators

### basic data type

- number
- string

**`**(backtick 反引号)
escaping  转义 **\n**
concatenate: "con" **+** "cat" + "e" + "nate"
template literals:\_ \_`half of 100 is **${**100 / 2**}**` `${xxx}`内的 xxx 会计算值
Unary operators(一元运算符)：**typeOf **"x"

- Boolean
- null
- undefined
- symbol

short-circuit evaluation 短路逻辑

- a || b : a 为真则返回 a,否则返回 b
- a && b : a 为假则返回 a,否则返回 b

## Program Structure

A fragment of code that produces a value is called an** *expression***.
If an expression corresponds to a sentence fragment, a JavaScript **_statement_** corresponds to a full sentence.
A program is a list of statements.

The simplest kind of statement is an expression with a semicolon after it. **1;**
**a binding, or variable:**

```javascript
let caught = 5 * 5;
```

You should imagine bindings as **tentacles**, rather than boxes. They do not *contain* values; they *grasp* them—two bindings can refer to the same value.

The collection of bindings and their values that exist at a given time is called the **environment. **

Executing a function is called **_invoking_**, **_calling_**, or **_applying_** it

console.log

```javascript
let x = 30;
console.log("the value of x is", x);
// → the value of x is 30
```

When a function produces a value, it is said to **_return_** that value.

```javascript
Math.max(2, 1, 3, 5, 9);
// 9
Math.min(2, 1, 3, 5, 9);
// 1
```

**braces** (`{` and `}`)
The braces can be used to group any number of statements into a single statement, called a** *block***.

indent 2 spaces

### exercises

#### 1. 打出三角形阵列

```javascript
for (let i = "#"; i.length < 8; i += "#") console.log(i);
```

#### 2. FizzBuzz

```javascript
for (let i = 1; i <= 100; i++) {
  let output = "";
  if (i % 3 === 0) output += "Fizz";
  if (i % 5 === 0) output += "Buzz";
  console.log(output || i);
}
```

#### 3. 象棋盘

```javascript
let size = 8;
for (let i = 0; i < size; i++) {
  let output = "";
  for (let j = 0; j < size; j++) {
    if ((i + j) % 2 === 0) output += " ";
    else output += "#";
  }
  console.log(output);
}
```
# Eloquent JavaScript(chapter 3)

## Function
A `return` keyword without an expression after it will cause the function to return `undefined`. Functions that don’t have a `return` statement at all, similarly return `undefined`.
#### Bingdings
Bindings declared with `let` and `const` are in fact local to the _block_ that they are declared in, so if you create one of those inside of a loop, the code before and after the loop cannot “see” it.
![image.png](https://cdn.nlark.com/yuque/0/2020/png/1753813/1597106785658-bfe4e160-d0bf-4c22-84fd-7fe30524ea6c.png#align=left&display=inline&height=214&margin=%5Bobject%20Object%5D&name=image.png&originHeight=214&originWidth=481&size=17477&status=done&style=none&width=481)
在for()内用let声明的变量，其scope在{}内

#### 函数提升
```javascript
console.log("The future says:", future());

function future() {
  return "You'll never have flying cars";
}
```
#### Arrow functions
```javascript
const power = (base, exponent) => {
  let result = 1;
  for (let count = 0; count < exponent; count++) {
    result *= base;
  }
  return result;
};

// 下面两个等价
const square1 = (x) => { return x * x; };
const square2 = x => x * x;
```
#### Optional arguments
```javascript
function fn(a, b) {do something}

fn(a,b,c,d)   // 传多的参数会被忽略
fn(a)  // 少传的参数为undefined

function fn(a, b = 2) // 设置默认值
{do something}   
```
#### The call stack
```javascript
function chicken() {
  return egg();
}
function egg() {
  return chicken();
}
console.log(chicken() + " came first.");
// → ??
```
#### Closure闭包
```javascript
function wrapValue(n) {
  let local = n;
  return () => local;
}

// wrap1和wrap2是wrapValue返回的函数
let wrap1 = wrapValue(1);
let wrap2 = wrapValue(2);
console.log(wrap1());
// → 1
console.log(wrap2());
// → 2


function multiplier(factor) {
  return number => number * factor;
}

let twice = multiplier(2);
console.log(twice(5));
// → 10
```
This feature—being able to reference a specific instance of a local binding in an enclosing scope—is called **_closure_**. A function that references bindings from local scopes around it is called _a_ **closure**.

A good mental model is to think of function values as containing both the code in their body and the **environment **in which they are created. When called, the function body sees the environment in which it was created, not the environment in which it is called.

#### Recursion递归
```javascript
function findSolution(target) {
  function find(current, history) {
    if (current == target) {
      return history;
    } else if (current > target) {
      return null;
    } else {
      return find(current + 5, `(${history} + 5)`) ||
             find(current * 3, `(${history} * 3)`);
    }
  }
  return find(1, "1");
}

console.log(findSolution(24));
// → (((1 * 3) + 5) * 3)
```
### exercises
#### 1. minimum
```javascript
let min = (a,b) => a > b ? b : a;

console.log(min(0, 10));
console.log(min(0, -10));
```
#### 2. isEven
```javascript
function isEven(x) {
  if (x === 0) return true
  else if (x === 1) return false
  else if (x < 0) return isEven(-x)
  else return isEven(x - 2)
}

console.log(isEven(50));
// → true
console.log(isEven(75));
// → false
console.log(isEven(-1));
```
#### 3. Bean counting
```javascript
function countBs(str) {
  return countChar(str, 'B')
}

function countChar(str, char) {
   let count = 0
  for (let i = 0; i < str.length; i++)
    if (str[i] === char) count += 1
  return count
}

console.log(countBs("BBC"));
// → 2
console.log(countChar("kakkerlak", "k"));
// → 4
```


