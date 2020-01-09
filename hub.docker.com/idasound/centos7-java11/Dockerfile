FROM centos:7

MAINTAINER Brand Idasound "haowang@idasound.com"


RUN rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime #修改时区 
RUN yum -y install kde-l10n-Chinese && yum -y install glibc-common #安装中文支持  
ENV LC_ALL zh_CN.utf8 #设置环境变量
RUN localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 #配置显示中文

# Do not use alias cp
RUN   yum install -y java-11-openjdk* 
