FROM docker.io/centos:7

ENV BUILD_DEPS="epel-release \
                net-tools \
                nscd \
                sudo \
                unzip \
                which"

RUN yum clean all && yum makecache fast                                      && \
    yum -y update                                                            && \
    yum -y install ${BUILD_DEPS}                                             && \
    yum clean all                                                            && \
    rm -rf /var/log/anaconda /anaconda-post.log /var/lib/yum

#向容器安装中文编码支持
RUN  yum -y install kde-l10n-Chinese          && \  
     yum -y reinstall glibc-common            && \  
     yum clean all                            && \  
     localedef -c -f UTF-8 -i zh_CN zh_CN.utf8   

#设置容器编码格式
ENV LC_ALL "zh_CN.UTF-8" 

RUN sed -i "s/^Defaults    env_reset/Defaults    !env_reset/g"     /etc/sudoers    && \
    sed -i "s/^Defaults    env_keep/#Defaults    env_keep/g"       /etc/sudoers    && \
    sed -i "s/^Defaults    secure_path/#Defaults    secure_path/g" /etc/sudoers   

#设置应用运行帐号
ENV AppUser=worker   \
    AppGroup=worker  

#设置目录
ENV AppRoot=/app     \
    RunRoot=/work   

RUN mkdir -p ${RunRoot}/logs                                             && \
    mkdir -p ${RunRoot}/code                                             && \
    mkdir -p ${AppRoot}                                                  && \
    groupadd -g 1000 ${AppGroup}                                         && \
    useradd -g 1000 -u 1000 ${AppUser}                                   && \
    chown -R ${AppUser}:${AppGroup} ${RunRoot}                           && \      
    echo ${AppUser}"    ALL=(ALL)    NOPASSWD: ALL" >> /etc/sudoers

#设置运行用户及用户组
USER ${AppUser}:${AppGroup}

WORKDIR ${RunRoot}

CMD ["/bin/bash"]


