# 第二章拓展 Linux阿里云ECS的安装部署

## 学习目标

- 了解阿里云ECS
- 购买阿里云服务器
- 使用XShell远程连接ECS
- 了解 ECS与虚拟机的区别
- 认识阿里云ECS的安全组机制

# 第一节 ECS是什么

​      云服务器 ECS（Elastic Compute Service）是一种安全可靠、弹性可伸缩的云计算服务，帮助用户降低 IT 成本，提升运维效率，使用户更专注于核心业务创新。

​      支持包年包月，按量付费等多种购买方式。更有利于生产开发中弹性扩容服务器数量。自动化的安装部署加维护，也让使用变得更加便捷。

![](image\Snipaste_2023-11-07_14-14-12.png)

# 第二节 购买ECS

​      点击产品ECS进入到阿里云购买页面。

![](image\Snipaste_2023-11-07_14-15-57.png)

​      选择购买类型为抢占式实例，相对比较便宜。选择地域接近的物理地址，延迟比较低。使用默认的交换机。

![](image\Snipaste_2023-11-07_14-19-20.png)

​    选择硬件配置，使用推荐的经济型就可以完成Linux的学习。

![](image\Snipaste_2023-11-07_14-20-42.png)

​    选择不要自动释放，由用户手动控制释放。

![](image\Snipaste_2023-11-07_14-22-33.png)

​    设置使用的网络类型，推荐使用流量付费，相对比较便宜。

![](image\Snipaste_2023-11-07_14-23-38.png)

​    填写root用户的密码用于登录使用，之后确认协议即可下单。

![](image\Snipaste_2023-11-07_14-24-51.png)

​    之后在控制台就能看到对应购买完成的服务器

![](image\Snipaste_2023-11-07_15-14-05.png)

# 第三节 使用XShell远程连接

​      打开XShell编译几个新的连接

![](image\Snipaste_2023-11-07_15-33-51.png)

​    同时点击用户认证页面，添加用户名和密码。

![](image\Snipaste_2023-11-07_15-35-07.png)

​    实际生产开发中，会一次性采购多台阿里云ECS，由于公网IP都是随机发布的，为了使用方便一般会使用hosts文件映射。

​    windows电脑的hosts文件在路径C:\Windows\System32\drivers\etc下面。

![](image\Snipaste_2023-11-07_15-37-59.png)

​    使用管理员权限打开一个文本编辑器

![](image\Snipaste_2023-11-07_15-38-49.png)

之后修改内容到hosts文件末尾即可

```text
#-------- 公共配置 --------

# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost

121.40.184.76	aliyun200
```

​    之后连接ECS的ip地址就可以全部替换为aliyun200

​    ![](image\Snipaste_2023-11-07_15-40-15.png)

# 第四节 认识修改ECS的安全组设置

​    可以在阿里云页面修改ECS的主机名称，保持在阿里云页面的对应关系。

![](image\Snipaste_2023-11-07_15-51-28.png)

修改完成之后重启ECS服务器生效。

![](image\Snipaste_2023-11-07_15-52-08.png)

  阿里云安全组是一种虚拟防火墙，用于控制安全组内 ECS实例的入流量和出流量。因为在实际的生产开发中，是不可能将防火墙关闭掉的，所有的端口放开都需要进行单独的配置。

![](image\Snipaste_2023-11-07_15-55-01.png)

​    配置的参数主要有两个，一个是放开的端口号，一个是运行访问的ip地址。

![](image\Snipaste_2023-11-07_15-58-53.png)

请根据实际场景设置授权对象的CIDR，另外，0.0.0.0/0或者掩码为0，代表允许或拒绝所有IP的访问，设置时请务必谨慎。





