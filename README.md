# B站动态抽奖程序
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Feigeen%2Fbili-bonus.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Feigeen%2Fbili-bonus?ref=badge_shield)


## 介绍

Python版本：基于Python3.9开发，建议版本>=3.6

程序版本：0.1.0-210222-a1

作者：我自己（@Eigeen）

调用的外部模块：

- requests
- lxml



## 功能

当前可用功能：

- 获取动态的转发数据，包括转发用户UID，用户名，转发内容
- 动态转发抽奖，数据导出为txt和csv(可用Excel打开)
- 基于MD5的可溯源高级抽奖方法，保证公正，较难黑箱

计划实现的功能：

- [ ] 动态评论抽奖
- [ ] 同时转发和评论的筛选



## 使用方法

### 安装外部模块

执行`pip install -r requirements.txt`

或运行Install_requirements.bat

### 使用

直接运行主目录下的`start_luckydraw.py，根据命令行提示输入参数，文件导出至data目录内。



## 关于抽奖方案

### MD5

简单来说，MD5通常用于计算多组数据是否相同，若两组数据不相同，那么这两组数据对应的MD5几乎完全不同，可视为随机数。相同数据的MD5一定相同。

### 评论数据构造

*抽奖前已去除重复项。

> 数据结构：`(id, uid, uname, content, timestamp)salt`
>
> 数据样例：`(1, 8381620, '瑞狩是只喵', '好可爱！！！[tv_大哭][tv_大哭]', 1610104107)477862261840413245`

结构解析：

- id：根据抓取顺序生成，从1开始。由于重复项的去除，实际导出的数据可能会少一部分id。
- salt：使用原动态id

### 标准数据构造

标准数据采用关键词"python"的全网指数，源页面：[https://index.chinaz.com/python/7](https://index.chinaz.com/python/7)，日期为抽奖当天日期的前七天。

> 数据样例：`2021-02-05_python_67,823`
>
> MD5：`b10f3543f3663984574dbc570b959b53`

### 判断方式

将评论和标准数据的MD5转为10进制整数，评论MD5最接近标准数据MD5，则为中奖。所有评论的数据会依照MD5的差值递增排序，若抽取5名，则前五名为中奖者。

## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Feigeen%2Fbili-bonus.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Feigeen%2Fbili-bonus?ref=badge_large)