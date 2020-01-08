FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive
ENV INITRD No
ENV LANG en_US.UTF-8

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        cmake \
        subversion \
        git \
        libcurl3 \
        freeglut3 \
        freeglut3-dev \
        libglew1.5-dev \
        libglu1-mesa \
        libglu1-mesa-dev \
        libgl1-mesa-glx \
        libgl1-mesa-dev \
        libfreetype6 \
        libfreetype6-dev \
        zlibc \
        zlib1g \
        zlib1g-dev \
        libgdal-dev \
        libsdl2-dev \
        libpng-dev \
        libtiff5-dev \
        qt5-default \
        libalut-dev \
        libogg-dev \
        libvorbis-dev \
        libvorbisfile3 \
        zip \
        unzip \
        vim.tiny wget curl sudo net-tools pwgen \
        git-core logrotate software-properties-common \
        openjdk-8-jre-headless && \
    locale-gen en_US en_US.UTF-8 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget -qO - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add - && \
    echo 'deb http://pkg.jenkins-ci.org/debian binary/' \
      | tee /etc/apt/sources.list.d/jenkins.list && \
    apt-get update && \
    apt-get install --no-install-recommends -y jenkins && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    update-rc.d -f jenkins disable

ENV JENKINS_HOME /var/lib/jenkins

USER jenkins

EXPOSE 8080 50000

VOLUME /var/lib/jenkins

CMD ["/usr/bin/java", "-jar", "/usr/share/jenkins/jenkins.war"]