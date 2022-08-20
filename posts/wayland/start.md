---
title: "Start"
date: 2022-08-14T16:28:12+08:00
---



apt install dev-wlroots-0.15.1 配置下环境

单独找到 tinywl 执行 make，晃下鼠标，好了报错

> No free output buffer slot

从 gitlab 下载对应版本 release

```
meson --buildtype debug build/
ninja -C build
```

从 build/ 找到生成的动态链接库 + 别名软链接，复制到 demo 文件夹里

```
export LD_LIBRARY_PATH=./
```

开始 debug，发现弄不出来，全是对象实例化与对象的方法绑定，猜测报错发生在绑定的函数指针里

---

还是把 wayland-book 看完再搞比较好。。