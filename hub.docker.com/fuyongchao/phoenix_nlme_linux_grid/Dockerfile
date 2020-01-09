# 指定操作系统
FROM centos:7.6.1810
# 指定作者信息
MAINTAINER fu_yongchao "3212418315@qq.com"
# 设置yum源，并安装基础的依赖环境
RUN yum -y install epel-release && \
    yum -y install gcc ksh R libxml2-devel nfs-utils openssh-server openssh-clients net-tools && \
	yum clean all
# 安装必须的R包	
RUN R -e "options(repos = \
    list(CRAN = 'http://mran.revolutionanalytics.com/snapshot/2019-08-06/')); \
    install.packages(c('batchtools', 'XML', 'reshape'))"
# 本地安装Certara.NLME8的R包
RUN mkdir -p /var/tmp/nlme/store
COPY Certara.NLME8_0.0.1.0001.tar.gz /var/tmp/nlme/store/Certara.NLME8_0.0.1.0001.tar.gz
RUN cd /var/tmp/nlme/store/ && \
    R CMD INSTALL Certara.NLME8_0.0.1.0001.tar.gz
# 新增用户用于后期提交任务# 启动SSH服务
RUN useradd -o -u 0 -g 0 -M -d /root -s /bin/bash submit && \
    echo 'submit:Qq123456' | chpasswd && \
    /usr/sbin/sshd-keygen -A
CMD ["/usr/sbin/sshd","-D"]