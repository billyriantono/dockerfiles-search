FROM centos 

LABEL MAINTAINER 'liwang <2859413527@QQ.COM>'

# 设置gitblit版本的环境变量
ENV GITBLITVERSION 1.8.0

# 从官网将其gitblit下载至容器的/目录下
ADD http://dl.bintray.com/gitblit/releases/gitblit-${GITBLITVERSION}.tar.gz /gitblit-${GITBLITVERSION}.tar.gz

# 将工作目录设置 / 
WORKDIR /

# 使用yum安装openjdk
RUN yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel

# 对下载的gitblit进行解压
# 解压完毕后删除刚刚下载的压缩包
# 修改gitblit配置文件的httpPort和repositoriesFolder
RUN set -x \
        && tar xf gitblit-${GITBLITVERSION}.tar.gz \
        && rm -f gitblit-${GITBLITVERSION}.tar.gz \
        && cd gitblit-${GITBLITVERSION}/data \
        && mkdir /git \
        && sed -i 's/server.httpPort = 0/server.httpPort = 9010/g' defaults.properties \
        && sed -i 's#git.repositoriesFolder = ${baseFolder}/git#git.repositoriesFolder = /git#g' defaults.properties

# 将工作目录设置为刚刚解压的gitblit目录中
WORKDIR /gitblit-${GITBLITVERSION}

# 开放 9010 和 29418 端口
EXPOSE 9010
EXPOSE 29418

# 启动gitblit
CMD ["/usr/bin/java","-jar","gitblit.jar","--baseFolder","data"]
