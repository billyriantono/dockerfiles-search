FROM scaleway/ubuntu:armhf-xenial
LABEL authors="Selenium <selenium-developers@googlegroups.com>"
MAINTAINER Scaleway <opensource@scaleway.com> (@scaleway)

# Prepare rootfs for image-builder
RUN /usr/local/sbin/scw-builder-enter

# Install JAVA8
RUN echo | add-apt-repository ppa:webupd8team/java                                         \
 && apt-get -q update                                                                      \
 && apt-get --force-yes -y -qq upgrade                                                     \
 && echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections  \
 && apt-get --force-yes -y -q install oracle-java8-installer                               \
 && apt-get clean

RUN apt-get --force-yes -y -q install \
    bzip2 \
    ca-certificates \
    openjdk-8-jre-headless \
    tzdata \
    sudo \
    unzip \
    wget  \
    && apt-get clean

# Patch rootfs
COPY ./overlay/ /

#================================================
# Customize sources for apt-get
#================================================
#RUN  echo "deb http://archive.ubuntu.com/ubuntu xenial main universe\n" > /etc/apt/sources.list \
#  && echo "deb http://archive.ubuntu.com/ubuntu xenial-updates main universe\n" >> /etc/apt/sources.list \
#  && echo "deb http://security.ubuntu.com/ubuntu xenial-security main universe\n" >> /etc/apt/sources.list

# No interactive frontend during docker build
#ENV DEBIAN_FRONTEND=noninteractive \
#    DEBCONF_NONINTERACTIVE_SEEN=true

#========================
# Miscellaneous packages
# Includes minimal runtime used for executing non GUI Java programs
#========================
#RUN apt-get -qqy update \
#  && apt-get -qqy --no-install-recommends install \
#    bzip2 \
#    ca-certificates \
#    openjdk-8-jre-headless \
#    tzdata \
#    sudo \
#    unzip \
#    wget \
#  && rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
#  && sed -i 's/securerandom\.source=file:\/dev\/random/securerandom\.source=file:\/dev\/urandom/' ./usr/lib/jvm/java-8-openjdk-amd64/jre/lib/security/java.security



#===================
# Timezone settings
# Possible alternative: https://github.com/docker/docker/issues/3359#issuecomment-32150214
#===================
ENV TZ "UTC"
RUN echo "${TZ}" > /etc/timezone \
  && dpkg-reconfigure --frontend noninteractive tzdata

#========================================
# Add normal user with passwordless sudo
#========================================
RUN useradd seluser \
         --shell /bin/bash  \
         --create-home \
  && usermod -a -G sudo seluser \
  && echo 'ALL ALL = (ALL) NOPASSWD: ALL' >> /etc/sudoers \
  && echo 'seluser:secret' | chpasswd

#===================================================
# Run the following commands as non-privileged user
#===================================================
USER seluser

#==========
# Selenium
#==========
RUN  sudo mkdir -p /opt/selenium \
  && sudo chown seluser:seluser /opt/selenium \
  && wget --no-verbose https://selenium-release.storage.googleapis.com/3.4/selenium-server-standalone-3.4.0.jar \
    -O /opt/selenium/selenium-server-standalone.jar


# Clean rootfs from image-builder
RUN /usr/local/sbin/scw-builder-leave
