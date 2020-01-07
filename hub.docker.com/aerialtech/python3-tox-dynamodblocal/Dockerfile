FROM python:3.6.7-slim-stretch

USER root

ENV DEBIAN_FRONTEND=noninteractive \
    TERM=linux \
    INITRD=No \
    LANGUAGE=en_US.UTF-8 \
    LANG=en_US.UTF-8  \
    LC_ALL=en_US.UTF-8 \
    LC_CTYPE=en_US.UTF-8 \
    LC_MESSAGES=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    GOSU_VERSION=1.9 \
    TINI_VERSION=v0.13.2 \
    TOX_VERSION=3.2.1

#add root asset (aliases and fix user id)
ADD files/* /root/


# Install curl, locales, apt-utils, gosu and tini
# create en_US.UTF-8
# update distribution package
# add few common alias to root user
# add utilities (create user, post install script)
# create airdock user list
RUN set -x && \
  apt-get update -qq && \
  apt-get install -y \
    apt-utils \
    curl \
    locales \
    build-essential \
    git && \
    /root/post-install

# The mkdir statement is necessary, more info here:
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN set -x && \
  mkdir -p /usr/share/man/man1 && \ 
  apt-get update -qq && \
  apt-get install -y \
  default-jdk && \ 
  apt-get install -y --no-install-recommends ca-certificates wget vim && \
  sed -i 's/^# en_US.UTF-8 UTF-8$/en_US.UTF-8 UTF-8/g' /etc/locale.gen && locale-gen && \
  update-locale LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 && \
  apt-get update -y && \
  dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')"  && \
  wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch"  && \
  wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc"  && \
  export GNUPGHOME="$(mktemp -d)"  && \
  echo "disable-ipv6" >> "${GNUPGHOME}/dirmngr.conf" && \
  gpg --no-tty --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4  && \
  gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu  && \
  rm -r /usr/local/bin/gosu.asc  && \
  chmod +x /usr/local/bin/gosu  && \
  gosu nobody true  && \
  wget -O /usr/local/bin/tini "https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini" && \
  wget -O /usr/local/bin/tini.asc "https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini.asc" && \
  gpg --no-tty --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 595E85A6B1B4779EA4DAAEC70B588DFF0527A9B7 && \
  gpg --batch --verify /usr/local/bin/tini.asc /usr/local/bin/tini  && \
  rm -r "$GNUPGHOME" /usr/local/bin/tini.asc  && \
  chmod +x /usr/local/bin/tini  && \
  apt-get purge -y --auto-remove wget  && \
  mv /root/aliases /root/.aliases && \
  echo "source ~/.aliases" >> /root/.bashrc && \
  /root/create-user java 4205 java 4205 && \
  /root/create-user py 4206 py 4206 && \
  /root/create-user docker 4242 docker 4242 && \
  /root/post-install

# Define default workdir
WORKDIR /root

# This part requires that the current folder contains the specific jdk tar file.
# Visit https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html to download
# the appropriate version.

# Add java dynamic memory script
COPY java-dynamic-memory-opts /srv/java/
COPY dynamodb_local_latest.tar.gz /tmp/

# Define commonly used JAVA_HOME variable
# Add /srv/java and jdk on PATH variable
ENV JAVA_HOME=/srv/java/jre \
    PATH=${PATH}:/srv/java/jdk/jre/bin:/srv/java

# Expose DynamoDB local port
EXPOSE 8000

# Prepare for build and tests
RUN pip install tox==${TOX_VERSION}

# Define default command.
CMD ["bash"]docker build -t aerialtech/debian-python3-tox-dynamodb .

# BUILD IT
#  docker build -t aerialtech/debian-python3-tox-dynamodb .
# RUN IT
#  docker run -it --rm -p 8000:8000 aerialtech/debian-python3-tox-dynamodb
