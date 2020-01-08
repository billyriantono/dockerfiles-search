FROM centos:7
MAINTAINER zhfang zhfang@dataman-inc.com

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && rm -rf /etc/yum.repos.d/* \
    && curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo \

