---
title: "DRM"
date: 2022-11-05T21:07:20+08:00
---

[Direct Rendering Manager](https://jan.newmarch.name/Wayland/DRM/)

### `static int modeset_open(int *out, const char *node)`

```c
int fd = open(node, O_RDWR | O_CLOEXEC);
```

把硬件当作文件操作，`O_RDWR`可读可写，`O_CLOEXEC`代表 close-on-exec 【】

```c
int ret = drmGetCap(fd, DRM_CAP_DUMB_BUFFER, &has_dumb);
```

询问驱动是否支持某功能，`&has_dumb` 返回结果

### `static int modeset_prepare(int fd)`

```c
drmModeRes *res = drmModeGetResources(fd);
```

获取 DRM 相关的 connector、CRTC 等相关信息

```c
drmModeConnector *conn = drmModeGetConnector(fd, res->connectors[i]);
```

### `static int modeset_setup_dev(int fd, drmModeRes *res, drmModeConnector *conn, struct modeset_dev *dev);`

显卡的 CRTC 控制其上的 connector，前者可能比后者数量少，显示屏可能非独立驱动。
