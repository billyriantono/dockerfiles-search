FROM mysql:5.6

MAINTAINER lewis@technoplusit.co.uk

# Install Java.
RUN \
  echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list && \
  echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
  apt-get update

RUN \
  echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  apt-get install -y oracle-java8-installer &&\
  apt-get clean

RUN echo "JAVA_HOME=/usr/lib/jvm/java-8-oracle" >> /etc/environment
ENV JAVA_HOME=/usr/lib/jvm/java-8-oracle

RUN \
  apt-get install -y curl unzip procps &&\
  apt-get clean

ENV GRADLE_VERSION 2.3
ENV GRADLE_ROOT /opt
ENV GRADLE_HOME /opt/gradle
ENV GRADLE_BIN /usr/bin/gradle
WORKDIR "$GRADLE_ROOT"

RUN curl -O -Ls "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
    && unzip "gradle-${GRADLE_VERSION}-bin.zip" \
    && ln -s "gradle-${GRADLE_VERSION}" gradle \
    && ln -s "${GRADLE_HOME}/bin/gradle" "${GRADLE_BIN}"

VOLUME ["/root/.gradle/caches"]
VOLUME ["/code"]
WORKDIR /code

ADD gradle_entrypoint.sh /gradle_entrypoint.sh

ENTRYPOINT ["/gradle_entrypoint.sh"]