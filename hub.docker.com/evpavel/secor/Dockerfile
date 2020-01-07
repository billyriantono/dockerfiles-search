FROM anapsix/alpine-java:8_jdk

RUN apk update && apk upgrade && \
    apk add curl wget && \
    rm -rf /var/cache/apk/*

ENV GRADLE_VERSION 4.5.1
ENV GRADLE_HOME /usr/lib/gradle/gradle-${GRADLE_VERSION}
ENV PATH ${PATH}:${GRADLE_HOME}/bin

WORKDIR /usr/lib/gradle
RUN set -x \
  && wget -q https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip \
  && unzip gradle-${GRADLE_VERSION}-bin.zip \
  && rm gradle-${GRADLE_VERSION}-bin.zip

# Hadoop
#RUN curl -Ls 'https://www.apache.org/dyn/closer.cgi?action=download&filename=hadoop/common/hadoop-2.7.5/hadoop-2.7.5.tar.gz' | tar -xz -C /usr/local/
#RUN ln -s /usr/local/hadoop-2.7.5 /usr/local/hadoop

#ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64
#ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:/usr/local/hadoop/lib/native
#ENV PATH $PATH:/usr/local/hadoop/bin
#
#RUN pip install --upgrade awscli

WORKDIR /

ADD . /app

RUN cd /app \
    && gradle shadowJar \
    && mkdir -p /opt/secor \
    && cp /app/build/libs/docker-secor-all.jar /opt/secor/secor.jar \
    && rm -rf /app \
    && rm -rf ~/.gradle

# Copy script to run Secor
COPY docker-entrypoint.sh /docker-entrypoint.sh

# Copy out properties files
COPY *.properties /opt/secor/

ENTRYPOINT ["/docker-entrypoint.sh"]

# used for temp-files that are uploaded
VOLUME /tmp
