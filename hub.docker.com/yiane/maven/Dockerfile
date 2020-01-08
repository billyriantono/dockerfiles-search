ARG JDK_VERSION=8
ARG MAVEN_VERSION=3
FROM maven:${MAVEN_VERSION}-jdk-${JDK_VERSION}

USER root

# 切换阿里源
ARG CHANGE_SOURCE=true
RUN if [ ${CHANGE_SOURCE} = true ]; then \
echo \
"deb http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch main non-free contrib\n\
deb http://mirrors.aliyun.com/debian-security stretch/updates main\n\
deb-src http://mirrors.aliyun.com/debian-security stretch/updates main\n\
deb http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib\n\
deb http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib\n\
deb-src http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib\n" > /etc/apt/sources.list \
#      && cat /etc/apt/sources.list \
;fi

###########################################################################
# Add a non-root user to prevent files being created with root permissions on host machine.
###########################################################################
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}

###########################################################################
# Set Timezone
###########################################################################

ARG TZ=Asia/Shanghai
ENV TZ ${TZ}
COPY settings.xml /usr/share/maven/ref/
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    groupadd -g ${PGID} www && \
    useradd -u ${PUID} -g www -m www -s /bin/bash && \
    apt-get update -yqq \
    && apt-get install -y --no-install-recommends \
    apt-utils \
    curl \
    wget \
    vim \
    inetutils-ping \
    libzip-dev zip unzip \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

ARG USER_HOME_DIR="/home/www"
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"
USER www
RUN mkdir -p /home/www/.m2

VOLUME ["/usr/src/mymaven", "/home/www/.m2"]

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
