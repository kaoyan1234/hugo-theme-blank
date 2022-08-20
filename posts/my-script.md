---
title: "My Script"
date: 2022-07-24T07:07:06+08:00
---

不知道第几次修改了 QAQ

# 数据

```lisp
;; 基础类型与 WASM 保持一致
;;
;; 1. 是否应该给 type 增加一个枚举类型？
;; 2. 非用户手动 nil 的出现就代表一个错误？
;; 3. 如果所有的变量都是引用，会产生多少性能损耗？

;; 新变量
;;
;; (类型)+ `:` + 变量名 + (修饰)
;; 修饰：`!` 不可变，`?` 可 nil
(i64:foo! 2)

;; 方法
;;
;; Put Set Get Delete
;; Put: RAW Set
;; Get: not for default

;; 复杂结构 TODO
;;
;; struct
;;
;; table
```

# 函数

```lisp
;; 定义
(void:foo (
    |i64:a (i64:b 1)|
    (fmt println a b)
))

;; 调用
(foo 2 3)

;; 接口
(interface:fmt
    ()
    ()
)

;; 方法
(impl bar for fmt
    ()
    ()
)
```

# 顺序

```lisp
;; 单行
(do
    (1 )
    (2 )
)

;; 并行
(go
    (- )
    (- )
)
```

# 分支

```lisp
;; 分支
(if true
    (true  do)
    (false do)
)

;; if + do == with
(with true
    (true 1 do)
    (true 2 do)
    (true 3 do)
)

;; if + elseif == when
(when enum:foo
    () ()
    () ()
       ()
)
```

# 循环

```lisp
;; 基础循环
(loop
    ()
    ()
    ()
)

;; 加点东西
;; 不同生命周期的条件
(while
    {() () ()}
    ()
    ...
)

;; for iter
(for |:k :v| (iter kv)
    (fmt println k v)
    (fmt println "next >> ")
)
```

# 包

```lisp
;; 加载
(import:std/fmt)

;; 卸载
(delete fmt)

;; 导出
(export:hello_world)
```

# 胡言乱语

```lisp
;; 虽然是惰性求值，但最终还是会计算
(+ 1 2)

;; 返回一个闭包，但不会执行
(quote (+ 1 2))

;; 简写个指针（bushi）
;; 有点不协调
&(+ 1 2)
```
