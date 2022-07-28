---
title: "My Script"
date: 2022-07-24T07:07:06+08:00
---

# 数据

## 数据类型

1. 是否应该给 type 增加一个枚举类型？

```
assert(type(int), type.int);
```

2. nil 的出现就代表一个错误

```
(do
    (:a 1)
    (println a) ;; 1
                ;; normal
)
(println a)     ;; nil
                ;; catch error
```

3. 如果所有的变量都是指针引用，那么会产生多大的性能损耗？

于不可变量、垃圾回收、运行时有什么关系？

引入关键词 dd 将变量和对象绑定？

## 数据结构

```
(table:foo .a 1 .b 2 .c 3)

(:auto_table {.a = 1 .b = 2 .c = 3})

(:auto_array {1 2 3})
```

# 函数

1. 是不是应该再编写程序的时候约定，我要的是什么变量，是复制过来还使用指针偷过来。调用时自动解引用

## 函数定义

```
(fn:new_func
    {}
    (do)
    (do)
)
```

## 函数调用

```
(func argu_a argu_b)
```

# 控制结构

## 分支

```
(if (empty a)
    (do)
)

;; if + do == when
(when (empty a)
    (do)
    (do)
    (do)
)

;; if + fn == switch
(case
    () ()
    () ()
    ()
)
```

## 循环

```
(loop
    {
        (fn:begin (:index 0))
        (fn:catch
            (if (> index 10)
                (getout)
            )
        )
        (fn:done (print "all done"))
    }
    (do)
    (do)
)
;; do 同理
```

# 其他

## 迭代器

```
(each {:key :value} (pairs table_A)
    (do)
)
```

## 保护 & 胡言乱语

```
(+ 1 2)         ;; 虽然是惰性求值，但最终还是会计算

(quote (+ 1 2)) ;; 返回一个闭包，但不会执行

'(+ 1 2)        ;; 简写
```
