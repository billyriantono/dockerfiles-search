FROM frankqcc/jenkins

USER root
RUN sed -i s@deb.debian.org@mirrors.aliyun.com@g /etc/apt/sources.list \
    && sed -i s@security.debian.org@mirrors.aliyun.com@g /etc/apt/sources.list \
    && sed -i s@http.debian.net@mirrors.aliyun.com@g /etc/apt/sources.list \
    && echo "deb http://mirrors.ustc.edu.cn/debian/ stretch main" >> /etc/apt/sources.list \
    && echo "deb http://mirrors.ustc.edu.cn/debian/ stretch-updates main" >> /etc/apt/sources.list \
    && mkdir /home/download \
    && cd /home/download \
    && apt-get update \
    && apt-get -y install \
        apt-transport-https \
        ca-certificates \
        curl \
        sudo \
        unzip \
        software-properties-common \
    && wget https://dl.bintray.com/qameta/maven/io/qameta/allure/allure-commandline/2.8.1/allure-commandline-2.8.1.zip \
    && unzip allure-commandline-2.8.1.zip \
    && mv allure-2.8.1/ /opt/ \
    && ln -s /opt/allure-2.8.1/bin/allure /usr/local/sbin/ \
    && curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey \
    && add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
        $(lsb_release -cs) \
        stable"  \
    && apt-get update \
    && apt-get -y install docker-ce \
    && cd / \
    && rm -R /home/download \
    && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
USER jenkins
