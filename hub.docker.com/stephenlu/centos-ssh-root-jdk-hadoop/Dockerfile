FROM stephenlu/centos-ssh-root-jdk
MAINTAINER stephenlu
# hadoop
RUN curl -s http://www.eu.apache.org/dist/hadoop/common/hadoop-2.6.0/hadoop-2.6.0.tar.gz | tar -xz -C /usr/local/
#ln是linux中又一个非常重要命令，它的功能是为某一个文件在另外一个位置建立一个同不的链接，这个命令最常用的参数是-s:进行软链结(symbolic link)
#具体用法是：ln –s 源文件 目标文件
RUN cd /usr/local && ln -s ./hadoop-2.6.0 hadoop-2.6.0

ENV HADOOP_HOME /usr/local/hadoop-2.6.0
ENV PATH $HADOOP_HOME/bin:$PATH
