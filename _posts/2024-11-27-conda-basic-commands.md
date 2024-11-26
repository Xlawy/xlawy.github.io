---
title: Conda基础命令
date: 2024-11-27 03:10 +0800
categories: [Conda]
tags: [Conda, Commands]
description: Conda基础命令
---

# Conda自身相关

## 查询当前版本

```shell
conda --version
```

## 更新Conda

```shell
conda update conda
```

# Conda虚拟环境相关

## 查询所有虚拟环境

```shell
conda env list
conda info --envs
```

## 创建新的虚拟环境

```shell
conda create -name [env_name] python=x.x
```

## 切换虚拟环境

```shell
conda activate [env_name]
```

## 关闭虚拟环境

```shel
conda deactivate
```

## 删除虚拟环境

```shell
conda remove -name [env_name] --all
```

# Conda包管理相关

## 查看所有已安装的包

```shell
conda list # 查看当前环境已安装的包
conda list -name [env_name] # 查看指定环境已安装的所有包
```

## 安装包

```shell
conda install [package_name] # 在当前环境安装包
conda install -name [env_name] [package_name] # 在指定环境安装包
```

## 删除包

```shell
conda remove [package_name] # 删除当前环境的包
conda remove -name [env_name] [package_name] # 删除指定环境的包
```

## 查找包信息

```shell
conda search [package_name]
```

















https://blog.csdn.net/be_racle/article/details/124896246

![image-20241127001136098](https://cdn.jsdelivr.net/gh/Xlawy/ImageHosting/img/image-20241127001136098.png)

