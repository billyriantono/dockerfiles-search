# 基础镜像
FROM gotoeasy/ubuntu-desktop
# 维护者信息
MAINTAINER gotoeasy <gotoeasy@163.com>

# 环境变量
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
ENV MAVEN_HOME="/opt/apache-maven-3.6.1"
ENV GRADLE_HOME="/opt/gradle-5.6"
ENV PATH $PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin:$GRADLE_HOME/bin

# 安装
RUN apt-get update && apt-get install -y \
    # java
    openjdk-8-jdk ca-certificates-java \
    # git和svn
    git rabbitvcs-cli rabbitvcs-core rabbitvcs-gedit rabbitvcs-nautilus && \
    # eclipse安装指定版
    wget http://eclipse.c3sl.ufpr.br/technology/epp/downloads/release/2019-09/M2/eclipse-committers-2019-09-M2-linux-gtk-x86_64.tar.gz -O /tmp/eclipse.tar.gz -q && \
    tar -xf /tmp/eclipse.tar.gz -C /opt && \
    rm /tmp/eclipse.tar.gz && \
    # 创建eclipse桌面快捷方式
    echo '[Desktop Entry]' > /root/Desktop/eclipse.desktop && \
    echo 'Type=Application' >> /root/Desktop/eclipse.desktop && \
    echo 'Name=Eclipse' >> /root/Desktop/eclipse.desktop && \
    echo 'GenericName=Eclipse' >> /root/Desktop/eclipse.desktop && \
    echo 'Comment=Eclipse IDE' >> /root/Desktop/eclipse.desktop && \
    echo 'Exec= /opt/eclipse/eclipse' >> /root/Desktop/eclipse.desktop && \
    echo 'Icon= /opt/eclipse/icon.xpm' >> /root/Desktop/eclipse.desktop && \
    echo 'Terminal=eclipse' >> /root/Desktop/eclipse.desktop && \
    echo 'Categories=Eclipse;' >> /root/Desktop/eclipse.desktop && \
    # 可执行
    chmod +x /root/Desktop/eclipse.desktop && \
    # maven安装指定版
    wget http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz -O /tmp/maven.tar.gz -q && \
    tar -xf /tmp/maven.tar.gz -C /opt && \
    rm /tmp/maven.tar.gz && \
    # gradle安装指定版
    wget http://services.gradle.org/distributions/gradle-5.6-bin.zip -O /tmp/gradle.zip -q && \
    unzip -d /opt /tmp/gradle.zip && \
    rm /tmp/gradle.zip && \
    # nodejs安装最新稳定版
    apt-get install -y nodejs && \
    apt-get install -y npm && \
    npm install n -g && \
    n stable && \
    npm uninstall n -g && \
    apt-get clean
