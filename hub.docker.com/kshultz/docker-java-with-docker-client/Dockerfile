# Trying a newer one.
# FROM docker:18.02-dind
FROM docker:18.09-dind

# Defining default variables and build arguments
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000
ARG jenkins_user_home=/home/${user}

ENV JENKINS_USER_HOME=${jenkins_user_home} \
  LANG=C.UTF-8 \
  JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk \
  PATH=${PATH}:/usr/local/bin:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin \
  DOCKER_IMAGE_CACHE_DIR=/docker-cache \
  MAVEN_VERSION=3.5.4 \
  AUTOCONFIGURE_DOCKER_STORAGE=true

RUN set -x \
    && apk add --no-cache \
    bash \
    bzip2 \
    curl  \
    ca-certificates \
    gcompat \
    git \
    libxml2-utils \
    py-pip \
    openjdk8 \
    nodejs \
    tar \
    tini
  
  RUN set -x \
    && apk add -U --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing aufs-util \
    && pip install --no-cache-dir "docker-compose" \
    && git config --global user.email "kshultz@cloudbees.com" \
    && git config --global user.name "Karl Shultz"

# Set up default user for jenkins
RUN addgroup -g ${gid} ${group} \
  && adduser \
    -h "${jenkins_user_home}" \
    -u "${uid}" \
    -G "${group}" \
    -s /bin/bash \
    -D "${user}" \
  && echo "${user}:${user}" | chpasswd

# Adding the default user to groups used by Docker engine
# "docker" for avoiding sudo, and "dockremap" if you enable user namespacing
RUN addgroup docker \
  && addgroup ${user} docker \
  && addgroup ${user} dockremap

# Install the right version of maven, since that can't just be easy :(
RUN wget http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  tar -zxvf apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  rm apache-maven-$MAVEN_VERSION-bin.tar.gz && \
  mv apache-maven-$MAVEN_VERSION /usr/lib/mvn && \
  ln -s /usr/lib/mvn/bin/mvn /usr/bin/mvn

# Those folders should not be on the Docker "layers"
VOLUME ${jenkins_user_home} /docker-cache /tmp

# Default working directory
WORKDIR ${jenkins_user_home}

COPY ./entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
