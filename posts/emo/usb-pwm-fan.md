---
title: "USB PWM Fan"
date: 2022-07-21T09:23:06+08:00
---

**风扇**

| 4 Pin | 作用 |
| ----- | ---- |
| GND   | 接地 |
| 12V   | 电源 |
| Tach  | 测速 |
| PWM   | 调速 |

**USB**

电源、接地、两条数据线

# QA

PWM Signal (+5V)  
[Noctua PWM specifications white paper](https://noctua.at/pub/media/wysiwyg/Noctua_PWM_specifications_white_paper.pdf)

USB 能够提供 5V+3.3V

电脑能给 2.5W 应该足够小风扇功率

可能需要一个三极管，来把 USB 的差分信号转换为 PWM Signal

不过我不会硬件，抓个壮丁来帮我做好了 QAQ

（暂时没考虑测速）
