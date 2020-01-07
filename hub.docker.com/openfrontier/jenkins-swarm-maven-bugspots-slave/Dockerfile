FROM openfrontier/jenkins-swarm-maven-slave

MAINTAINER XJD <xing.jiudong@trans-cosmos.com.cn>

USER root
RUN set -ex \
        \
        && buildDeps=' \
                bison \
                dpkg-dev \
                libgdbm-dev \
                # ruby 2.3 on stretch can only support libssl1.0-dev (libssl dev from buildpack-deps is 1.1.x)
                libssl1.0-dev \
                gcc \
                cmake \
                ruby-dev \
                pkg-config \
                make \
                ruby \
        ' \
        && apt-get update \
        && apt-get install -y --no-install-recommends $buildDeps \
        && rm -rf /var/lib/apt/lists/*

RUN gem install bugspots

USER "${JENKINS_USER}"

