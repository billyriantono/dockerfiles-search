FROM gitlab/gitlab-ce

MAINTAINER madehao1983@sina.com

RUN set -x \
    && apt-get -y update \
    && apt-get -y upgrade \
    && apt-get -y install tzdata locales wget \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata \
    && apt-get clean \
    && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* \
    && localedef -f UTF-8 -i zh_CN zh_CN.UTF-8

RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
        "http://download.oracle.com/otn-pub/java/jdk/8u171-b11/512cd62ec5174c3487ac17c61aaa89e8/jdk-8u171-linux-x64.tar.gz" \
    && tar -zxvf jdk-8u171-linux-x64.tar.gz \
    && mkdir /usr/local/java/ \
    && mv jdk1.8.0_171 /usr/local/java/ \
    && chown -R root:root /usr/local/java \
    && rm -f jdk-8u171-linux-x64.tar.gz

ENV JAVA_HOME=/usr/local/java/jdk1.8.0_171 \
    CLASSPATH=.:/usr/local/java/jdk1.8.0_171/lib/dt.jar:/usr/local/java/jdk1.8.0_171/lib/tools.jar \
    PATH=$PATH:/usr/local/java/jdk1.8.0_171/bin

ENV TZ="Asia/Shanghai"

RUN mkdir /subgit
WORKDIR /subgit
RUN wget "https://subgit.com/files/subgit-3.3.2.zip" \
    && jar -xvf subgit-3.3.2.zip \
    && rm -f subgit-3.3.2.zip

ENV PATH=$PATH:/subgit/subgit-3.3.2/bin

WORKDIR /


