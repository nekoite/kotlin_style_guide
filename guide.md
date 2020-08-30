<h1 align="center">
  <br>
  Nekoite Kotlin Style Guide
  <h4 align="center">
    <a href="guide_cn.md">中文</a><br>
  </h4>
  <h5 align="center">
<img src="https://img.shields.io/badge/code-style-ff69b4"></img>
</h5>
  <br>
  <br>
</h1>

## 1 Introduction

This document serves as the complete definition of Nekoite's coding standards for source code in the Kotlin Programming Language.

## 2 Source file basics

### 2.1 File name

The source file name should be in Pascal Case (`PascalCase`), with the `.kt` extension.

If the source file contains **exactly** one class (including objects, classes, interfaces), then the name of the source file should be the same as the name of the class plus the `.kt` extension. Otherwise, the name should describe the functionality of the source file.

### 2.2 File encoding: `UTF-8`

Source files are encoded in **UTF-8**.

### 2.3 Special characters

#### 2.3.1 Whitespace characters

Aside from the line terminator sequence, the ASCII horizontal space character (0x20) is the only whitespace character that appears anywhere in a source file. This implies that:

1. All other whitespace characters in string and character literals are escaped.
2. Tab characters are **not** used for indentation.

#### 2.3.2 Special escape sequences

For any character that has a special escape sequence (`\b`, `\t`, `\n`, `\f`, `\r`, `\"`, `\'` and `\\`), that sequence is used rather than the corresponding octal (e.g. `\012`) or Unicode (e.g. `\u000a`) escape.

## 3 Code formatting

### 3.1 Braces

Branches for `when`, `if/else` does not need curly braces only when the branches can be placed in a single line. Anything other than that should add curly braces.

```kotlin
if (string.isEmpty()) return  // GOOD

if (string.isEmpty()) {
    return      // GOOD
} else return   // GOOD

if (true)
    return      // BAD

when (value) {
    0 -> return // GOOD
    1 -> {
        return  // GOOD
    }
    2 -> { return } // BAD
}
```

If there were to be any empty blocks, use curly braces on the same line with a space between them.

```kotlin
if (something) { }  // GOOD

if (something) {}   // BAD

if (something) {    // Not that good
}
```

### 3.2 Statements

No semicolons (`;`) after statements.

### 3.3 Line-wrapping

We don't define any column character limits, but we suggest to break when a line is long.

#### 3.3.1 Where to break

Break a line **before**

- operators and infix functions
- `.`, `?.`
- `::`

Break a line **after**

- `,`, `{`, `(`
- `->`
- `=` only when used in single expression functions and properties

### 3.4 Indentation

Use 4 spaces every level for indentation.

### 3.5 Function definitions

A single expression function (functions defined using `=` assignments) could be used **only when** the function body could be written in a single line.

```kotlin
fun myFun(a: Int) : Int = a + 1   // GOOD

fun myFun(a: Int) : Int =
    a + 1   // GOOD

fun myFun(a: Int) : ByteArray = ByteArray(a).apply {      // BAD
        println()
    }

fun myFun(a: Int) : ByteArray =
    ByteArray(a).apply { println() }  // GOOD

fun myFun(a: Int) : ByteArray {
    return ByteArray(a).apply {       // GOOD
        println()
    }
}
```

When the argument list of a function could not be fit on a single line, then each argument should be on a new line.

```kotlin
fun f(
    a: Int,
    b: Int = 3,
    c: Int = 4
): Int {
    return a + b + c
}
```

### 3.6 Properties

When initialization is too long, break the line after `=`. `get` and `set` declarations should be on different lines unless the property is readonly (`val`).

```kotlin
val p: Int =
    Db.db()["db3"].user("user").level()

var p: Int = 3
    get() {
        return doSomething(field)
    }
    set(value) {
        field = doSomething(value)
    }

val p: Int get() = 3
```

### 3.7 Whitespace

#### 3.7.1 Vertical whitespace

Always add a blank line at the end of the file.

Other rules are not specified. Use blank lines where proper to make code clear.

#### 3.7.2 Horizontal whitespace

Use a single space

- after `//`
- (or multiple spaces) before `//` only when used with code on the same line
- before `{`
- between `if`, `for`, `catch`, etc. and its matching `(`
- before and after any binary operators (including `->`) **but excluding**
  - `::`
  - `.`
  - `..`
- after `:`
- before `:` **only when** used in inheritance and generic constraints

### 3.8 Annotations

Put annotations wherever you like.

## 4 Documentation

See [KDoc][kdoc].


<br><hr>

### References

- [Kotlin Style Guide][kotlin_style_guide]
- [Google Java Style Guide][google_style_guide]




[kotlin_style_guide]: https://developer.android.com/kotlin/style-guide
[google_style_guide]: https://google.github.io/styleguide/javaguide.html
[kdoc]: https://kotlinlang.org/docs/reference/kotlin-doc.html
