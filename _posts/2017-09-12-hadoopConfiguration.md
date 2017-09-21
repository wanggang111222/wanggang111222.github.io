---
layout:     post
title:      hadoop的安装配置
subtitle:   适于hadoop初学者
date:       2017-09-12
author:     WG
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - java
    - hadoop
---
准备工作：把JDK和Hadoop安装包上传到linux系统（oracle用户的根目录）
# JDK安装
 
- **在oracle用户的根目录，Jdk解压，（hadoop用户操作**
{% highlight xml %}tar -zxvf jdk-8u65-linux-x64.tar.gz{% endhighlight %}
 解压完成后，在oracle用户的根目录有一个jdk1.8.0_65目录

- **配置环境变量，需要修改/etc/profile文件（root用户操作）**
切到root用户，输入su命令
{% highlight xml %}
vi /etc/profile
{% endhighlight %}
进去编辑器后，输入i，进入vi编辑器的插入模式
在profile文件最后添加
{% highlight xml %}
JAVA_HOME=/home/hadoop/jdk1.8.0_65
export PATH=$PATH:$JAVA_HOME/bin
{% endhighlight %}
 编辑完成后，按下esc退出插入模式 输入：，这时在左下角有一个冒号的标识q   退出不保存 wq保存退出q!   强制退出
- **把修改的环境变量生效（hadoop用户操作）**
执行
{% highlight xml %}
source /etc/profile
{% endhighlight %}
# Hadoop安装

- **在hadoop用户的根目录，解压（hadoop用户操作）**
{% highlight xml %}
tar -zxvf hadoop-2.6.0.tar.gz
{% endhighlight %}
解压完成在oracle用户的根目录下有一个hadoop-2.6.0目录

- **修改配置文件hadoop-2.6.0/etc/hadoop/hadoop-env.sh（hadoop用户操作）**
{% highlight xml %}
export JAVA_HOME=/home/hadoop/jdk1.8.0_65
{% endhighlight %}
- **修改配置文件hadoop-2.6.0/etc/hadoop/core-site.xml，添加（hadoop用户操作）**
{% highlight xml %}
<property>
         <name>fs.defaultFS</name>
         <value>hdfs://oracle:9000</value>
</property>
{% endhighlight %}
- **修改配置文件hadoop-2.6.0/etc/hadoop/hdfs-site.xml，添加（hadoop用户操作）**
{%highlight xml%}
<property>
        <name>dfs.replication</name>
         <value>1</value>
</property>
{%endhighlight%}
- **修改修改配置文件hadoop-2.6.0/etc/hadoop/mapred-site.xml（hadoop用户操作）**

这个文件没有，需要复制一份
{%highlight xml%}
cp etc/hadoop/mapred-site.xml.template etc/hadoop/mapred-site.xml
{% endhighlight %}
添加
{%highlight xml%}
<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>
{% endhighlight %}
- **修改配置文件hadoop-2.6.0/etc/hadoop/yarn-site.xml，添加（hadoop用户操作）**
{%highlight xml%}
<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle</value>
</property>
{% endhighlight %}
- **修改/etc/hosts文件（root用户操作）,添加：ip主机名称**
{%highlight xml%}
192.168.199.100  oracle
{% endhighlight %}
- **格式化HDFS，在hadoop解压目录下，执行如下命令：（hadoop用户操作）**
{%highlight xml%}
bin/hdfs namenode –format
{% endhighlight %}
注意：格式化只能操作一次，如果因为某种原因，集群不能用，需要再次格式化，需要把上一次格式化的信息删除，在/tmp目录里执行rm–rf *
- **启动集群，在hadoop解压目录下，执行如下命令：（hadoop用户操作）**
启动集群：sbin/start-all.sh需要输入四次当前用户的密码(通过配置ssh互信解决)
          启动后，在命令行输入jps有以下输出
{%highlight xml%}
[oracle@oracle hadoop-2.6.0]$ jps
32033 Jps
31718 SecondaryNameNode
31528 DataNode
31852 ResourceManager
31437 NameNode
31949 NodeManager
{% endhighlight %}
关闭集群：sbin/stop-all.sh需要输入四次当前用户的密码(通过配置ssh互信解决)
