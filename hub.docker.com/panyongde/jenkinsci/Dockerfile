FROM ubuntu:16.04

RUN apt-get update -y
RUN apt-get install -y software-properties-common
RUN apt-get install -y openssl openssh-client tar xz-utils wget git curl zip bzip2 
RUN rm -rf /var/lib/apt/lists/*

###########################################################################################################
# APT-FAST
###########################################################################################################

# RUN add-apt-repository ppa:saiarcot895/myppa
# RUN apt-get update -y
# RUN apt-get -y install apt-fast

###########################################################################################################
# JAVA 8
###########################################################################################################

RUN echo -e "" | add-apt-repository ppa:webupd8team/java
RUN apt-get update -y 
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
RUN apt-get install -y oracle-java8-installer
RUN apt-get install -y oracle-java8-set-default

###########################################################################################################
# JENKINS
###########################################################################################################

ENV JENKINS_HOME /home/jenkins
ENV JENKINS_SLAVE_AGENT_PORT 50000

# Jenkins is run with user `jenkins`, uid = 1000
# If you bind mount a volume from the host or a data container, 
# ensure you use the same uid
RUN mkdir -p /home/jenkins
RUN useradd -c "jenkins" jenkins -u 1000 -s /bin/bash -d "/home/jenkins"
RUN /bin/echo -e "jenkins\njenkins" | passwd jenkins
RUN adduser jenkins sudo

# Jenkins home directory is a volume, so configuration and build history 
# can be persisted and survive image upgrades

RUN echo "JAVA_HOME=/usr/lib/jvm/java-8-oracle/bin" >> /home/jenkins/.bsharc
RUN echo "export JAVA_HOME" >> /home/jenkins/.bsharc
RUN echo 'PATH=$PATH:$JAVA_HOME' >> /home/jenkins/.bsharc
RUN echo "export PATH" >> /home/jenkins/.bsharc
RUN chown jenkins -Rf /home/jenkins/

# `/usr/share/jenkins/ref/` contains all reference configuration we want 
# to set on a fresh new installation. Use it to bundle additional plugins 
# or config file with your custom jenkins Docker image.
RUN mkdir -p /usr/share/jenkins/ref/init.groovy.d


ENV JENKINS_VERSION 2.89.2

# could use ADD but this one does not check Last-Modified header 
# see https://github.com/docker/docker/issues/8331
RUN curl -fL http://mirrors.jenkins-ci.org/war-stable/$JENKINS_VERSION/jenkins.war -o /usr/share/jenkins/jenkins.war

ENV JENKINS_UC https://updates.jenkins-ci.org
RUN chown -Rf jenkins "$JENKINS_HOME" /usr/share/jenkins/ref

# for main web interface:
EXPOSE 8080

# will be used by attached slave agents:
EXPOSE 50000

ENV COPY_REFERENCE_FILE_LOG $JENKINS_HOME/copy_reference_file.log

# from a derived Dockerfile, can use `RUN plugins.sh active.txt` to setup /usr/share/jenkins/ref/plugins from a support bundle
# COPY plugins.sh /usr/local/bin/plugins.sh
# COPY plugins.txt /usr/share/jenkins/plugins.txt
# RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

COPY jenkins.sh /usr/local/bin/jenkins.sh
RUN chmod +x /usr/local/bin/jenkins.sh
RUN chown -Rf jenkins /home/jenkins/
RUN chmod -Rf 777 /home/jenkins/

###########################################################################################################
# GENERATE A SSH KEY
###########################################################################################################
RUN mkdir -p /home/jenkins/.ssh/ && \
    cd /home/jenkins/.ssh/ && \
    ssh-keygen -t rsa -b 4096 -C '' -f /home/jenkins/.ssh/id_rsa && \
    echo "StrictHostKeyChecking no" >>  /home/jenkins/.ssh/config && \
    echo "UserKnownHostsFile /dev/null" >>  /home/jenkins/.ssh/config &&\
    chown -Rf jenkins:jenkins /home/jenkins/ && \
    ssh-agent /bin/bash && eval "$(ssh-agent -s)" && \
    ssh-add /home/jenkins/.ssh/id_rsa

###########################################################################################################
# NODEJS
###########################################################################################################

# gpg keys listed at https://github.com/nodejs/node
RUN set -ex \
  && for key in \
    9554F04D7259F04124DE6B476D5A82AC7E37093B \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
  ; do \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
  done

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 8.9.3

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz"
RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc"
RUN gpg --verify SHASUMS256.txt.asc
RUN grep " node-v$NODE_VERSION-linux-x64.tar.xz\$" SHASUMS256.txt.asc | sha256sum -c -
RUN tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1
RUN rm "node-v$NODE_VERSION-linux-x64.tar.xz" SHASUMS256.txt.asc

RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN chown -Rf jenkins /usr/local/lib/node_modules


###########################################################################################################
# PHP 7
###########################################################################################################

RUN apt-get install -y language-pack-en-base
RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get -y update && apt-get -y upgrade && apt-get -y install snmp php7.1 \
    php7.1-bz2  \
    php7.1-mbstring \
    php7.1-cli  \
    php7.1-common  \
    php7.1-curl  \
    php7.1-dev  \
    php7.1-gd  \
    php7.1-imap  \
    php7.1-interbase  \
    php7.1-intl  \
    php7.1-json  \
    php7.1-ldap  \
    php7.1-mcrypt  \
    php7.1-mysql  \
    php7.1-odbc  \
    php7.1-opcache  \
    php7.1-pgsql  \
    php7.1-pspell  \
    php7.1-readline  \
    php7.1-recode  \
    php7.1-snmp  \
    php7.1-sqlite3  \
    php7.1-sybase  \
    php7.1-tidy  \
    php7.1-xmlrpc \
    php7.1-zip \
    php-mongodb \
    php-redis \
    php-apcu \
    php-amqp \
    php-memcached

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# RUN sudo pecl install mongodb
# RUN echo "extension=mongodb.so" > /etc/php/7.0/cli/conf.d/20-mongodb.ini

###########################################################################################################
# SQL LITE
###########################################################################################################
# RUN apt-get install sqlite3 libsqlite3-dev

###########################################################################################################
# ANSIBLE
###########################################################################################################
# RUN apt-add-repository -y ppa:ansible/ansible
# RUN apt-get -y update
# RUN apt-get -y install ansible openssh-client

###########################################################################################################
# ANSISTRANO
###########################################################################################################
# RUN ansible-galaxy install --force carlosbuenosvinos.ansistrano-deploy carlosbuenosvinos.ansistrano-rollback
# RUN adduser --disabled-password --gecos '' ansistrano
# RUN adduser ansistrano sudo
# RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

###########################################################################################################
# SDK
###########################################################################################################

# Installs i386 architecture required for running 32 bit Android tools
RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    apt-get install -y libc6:i386 zlib1g:i386 libncurses5:i386 libstdc++6:i386 lib32z1 wget unzip && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoremove -y && \
    apt-get clean

WORKDIR /opt

# Gradle
# ENV GRADLE_HOME /opt/gradle
# ENV GRADLE_VERSION 4.1
# ENV GRADLE_HASH 3014f027ae08bf3d9f7360e4e4352e80

# ENV PATH $PATH:$GRADLE_HOME/bin
# RUN wget -q "https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" && \
#     echo "${GRADLE_HASH} gradle-${GRADLE_VERSION}-bin.zip" > gradle-${GRADLE_VERSION}-bin.zip.md5 && \
#     md5sum -c gradle-${GRADLE_VERSION}-bin.zip.md5 && \
#     unzip -q "gradle-${GRADLE_VERSION}-bin.zip" && \
#     ln -s "gradle-${GRADLE_VERSION}" "${GRADLE_HOME}" && \
#     rm "gradle-${GRADLE_VERSION}-bin.zip"*

# Installs Android SDK
RUN dpkg --add-architecture i386 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get update && \
    apt-get install -yq build-essential libssl-dev ruby ruby-dev --no-install-recommends && \
    apt-get clean
    
RUN gem install bundler

# Download and untar Android SDK tools
RUN mkdir -p /usr/local/android-sdk-linux
RUN wget https://dl.google.com/android/repository/tools_r25.2.3-linux.zip -O tools.zip
RUN unzip tools.zip -d /usr/local/android-sdk-linux
RUN rm tools.zip

# Set environment variable
ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

RUN mkdir $ANDROID_HOME/licenses
RUN echo 8933bad161af4178b1185d1a37fbf41ea5269c55 > $ANDROID_HOME/licenses/android-sdk-license
RUN echo d56f5187479451eabf01fb78af6dfcb131a6481e >> $ANDROID_HOME/licenses/android-sdk-license
RUN echo 84831b9409646a918e30573bab4c9c91346d8abd > $ANDROID_HOME/licenses/android-sdk-preview-license

# Update and install using sdkmanager 
RUN $ANDROID_HOME/tools/bin/sdkmanager "tools" "platform-tools"
RUN $ANDROID_HOME/tools/bin/sdkmanager "build-tools;26.0.2" "build-tools;25.0.3"
RUN $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-26" "platforms;android-25" "platforms;android-24" "platforms;android-23"
RUN $ANDROID_HOME/tools/bin/sdkmanager "extras;android;m2repository" "extras;google;m2repository"
RUN $ANDROID_HOME/tools/bin/sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2"
RUN $ANDROID_HOME/tools/bin/sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2"

###########################################################################################################
# IONIC CORDOVA
###########################################################################################################
ENV CORDOVA_VERSION 7.1.0
WORKDIR "/tmp"
RUN npm i -g --unsafe-perm cordova@${CORDOVA_VERSION}

ENV IONIC_VERSION 3.19.0
RUN apt-get update && \
    npm i -g --unsafe-perm ionic@${IONIC_VERSION} && \
    ionic --no-interactive config set -g daemon.updates false && \
    rm -rf /var/lib/apt/lists/* && apt-get clean


###########################################################################################################
# Others
###########################################################################################################
RUN apt-get update && apt-get install -y git vim && apt-get clean

RUN gem install fir-cli
RUN npm install android-versions --save

###########################################################################################################
# docker
###########################################################################################################
RUN apt-get update && \
    apt-get -y install apt-transport-https \
      ca-certificates \
      curl \
      gnupg2 \
      software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
    add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
      $(lsb_release -cs) \
      stable" && \
    apt-get update && \
    apt-get -y install docker-ce && \
    curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose
    
###########################################################################################################
# EXPECT
###########################################################################################################
RUN apt-get install -y expect

###########################################################################################################
# CHANGE TO JENKINS USER
###########################################################################################################

USER jenkins
ENTRYPOINT ["/usr/local/bin/jenkins.sh"]
 
