FROM markadams/chromium-xvfb

#Proxy
#ARG HTTP_PROXY='http://172.17.0.1:3128/'
#ARG JDK_INSTALLER_PATH=/var/cache/oracle-jdk8-installer

#ENV http_proxy ${HTTP_PROXY}

#RUN echo 'Acquire::proxy "'${HTTP_PROXY}'";' >> /etc/apt/apt.conf && \
#    mkdir ${JDK_INSTALLER_PATH}
#    touch ${JDK_INSTALLER_PATH}/wgetrc && \
#    echo "use_proxy=yes" >> ${JDK_INSTALLER_PATH}/wgetrc && \
#    echo "http_proxy="${HTTP_PROXY} >> ${JDK_INSTALLER_PATH}/wgetrc && \
#    echo "https_proxy="${HTTP_PROXY} >> ${JDK_INSTALLER_PATH}/wgetrc && \
# ---

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
    echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
    apt-get update && \
    apt-get -y --no-install-recommends install oracle-java8-installer