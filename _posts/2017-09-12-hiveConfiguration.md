---
layout:     post
title:      hive的安装配置
subtitle:   适于hadoop初学者
date:       2017-09-12
author:     WG
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - java
    - hadoop
---
# Hive配置
- **安装MySQL**

        yum install mysql-server mysql mysql-devel

		
- **开启mysql**

        service mysqld start

- **设置root密码**

        mysqladmin -u root password 'root'
		
- **设置mysql开机启动**

        chkconfig mysqld on

- **解压hive**

- **修改hive-env.sh，从模板文件复制出来**

        export HADOOP_HEAPSIZE=1024
        # Set HADOOP_HOME to point to a specific hadoop install directory
        HADOOP_HOME=/home/hadoop/hadoop-2.4.1
        # Hive Configuration Directory can be controlled by:
        export HIVE_CONF_DIR=/home/hadoop/apache-hive-1.0.0-bin/conf
        # Folder containing extra ibraries required for hive compilation/execution can be controlled by:
        export HIVE_AUX_JARS_PATH=/home/hadoop/apache-hive-1.0.0-bin/lib
		
- **配置hive-site.xml**

- **拷贝mysql-connector-java-5.0.8-bin.jar到hive 的lib下面**

- **创建hive数据库 linux相关-->安装mysql**

- **把jline-2.12.jar拷贝到hadoop相应的目录下，替代jline-0.9.94.jar，否则启动会报错**

        cp hive/lib/jline-2.12.jar  hadoop-2.6.0/share/hadoop/yarn/lib/

- **bin/hive命令启动hive**
