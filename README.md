padavan 中文
=====

简体中文 & 路由器适配

------

padavan 是一个优秀的路由器固件，支持采用 RT3883/MT7620/MT7621/MT7628 等系列 CPU 的路由器

## 说明

本项目fork自 https://github.com/gorden5566/padavan

项目主要包含两部分：简体中文 dict 文件，部分常见路由器的适配文件

已适配的路由器型号如下：

- 联想 newifi mini

------

![image](https://github.com/KyonLi/padavan/raw/master/screenshot/index.png)

## 使用方法

### 手动编译固件

若需要更多定制功能，请自己修改源码编译固件。

## 编译步骤

### 环境准备

官方建议使用 ubuntu 16.04 LTS，你也可以使用 debian 衍生的其他 Linux 系统。

安装 git
``` bash
sudo apt-get update
sudo apt-get install git
```

安装依赖
``` bash
sudo apt-get install autoconf automake autopoint bison build-essential flex gawk gettext git gperf libtool pkg-config zlib1g-dev libgmp3-dev libmpc-dev libmpfr-dev texinfo python-docutils
```

### 获取 padavan 固件源码

``` bash
cd /opt
sudo git clone https://bitbucket.org/padavan/rt-n56u
```
如果下载比较慢，也可以从 oschina 镜像下载
``` bash
cd /opt
sudo git clone https://gitee.com/gorden5566/rt-n56u.git
```

### 安装简体中文

下载简体中文源码
``` bash
cd ~/
git clone https://github.com/KyonLi/padavan.git
```

安装
``` bash
cd ~/padavan
sudo sh ./install.sh
```
依次输入 1 和 2 复制文件到项目目录

### 编译交叉编译工具链

交叉编译工具链只需要编译一次即可
``` bash
cd /opt/rt-n56u/toolchain-mipsel
sudo ./clean_sources
sudo ./build_toolchain
```

### 配置修改

#### 方法一： 手动编辑 `/opt/rt-n56u/trunk/.config`

修改路由器型号相关配置
```
### Target Vendor/Product (support only Ralink RT3883/MT7620/MT7621/MT7628)
CONFIG_VENDOR=Ralink
CONFIG_PRODUCT=MT7620

### Target ProductID (board select, max 12 symbols)
CONFIG_FIRMWARE_PRODUCT_ID="RT-AC54U"
```

修改语言配置
```
CONFIG_FIRMWARE_INCLUDE_LANG_CN=y
```

#### 方法二： 使用编辑好的配置文件

``` bash
cd /opt/rt-n56u/trunk/
sudo cp configs/templates/newifi_mini_full.config .config
```

### 编译固件

执行如下命令编译固件
``` bash
cd /opt/rt-n56u/trunk
sudo ./clear_tree
sudo ./build_firmware
```

## 文件说明

```
├── configs
│   ├── boards
│   │   └── RT-AC54U ---newifi-mini适配文件
│   │       ├── board.h
│   │       ├── board.mk
│   │       ├── kernel-3.4.x.config
│   │       └── libc.config -> ../uclibc-mipsel.config
│   └── templates
│       ├── newifi_mini_base.config ---newifi-mini简版配置
│       └── newifi_mini_full.config ---newifi-mini完整版配置
└── user
    └── www
        ├── dict
        │   └── CN.dict ---简体中文语言文件
        └── Makefile
```

## 贡献列表

详见 [contributors](https://github.com/gorden5566/padavan/graphs/contributors)
