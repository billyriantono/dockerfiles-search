FROM openshift/base-centos7

ENV JAVA_VERSION 8u162
ENV BUILD_VERSION b12
ENV HASH_CODE 0da788060d494f5095bf8624735fa2f1


ENV GRADLE_VERSION 4.6

LABEL io.k8s.display-name="Gradle s2i Builder for openshift" \
      io.k8s.description="Platform for building and running Gradle applications" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="java8,gradle"

RUN yum -y upgrade \
    && yum -y install wget \
    && wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$BUILD_VERSION/$HASH_CODE/jdk-$JAVA_VERSION-linux-x64.rpm" -O /tmp/jdk-8-linux-x64.rpm \
    && yum -y install /tmp/jdk-8-linux-x64.rpm \
    && rm -rf /tmp/jdk-8-linux-x64.rpm \
    && yum -y clean all

RUN alternatives --install /usr/bin/java java /usr/java/latest/bin/java 200000 \
    && alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000 \
    && alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000 \
    && alternatives --install /usr/bin/keytool keytool /usr/java/latest/bin/keytool 200000


ENV JAVA_HOME /usr/java/latest

RUN curl -sL -0 https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o /tmp/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip /tmp/gradle-${GRADLE_VERSION}-bin.zip -d /usr/local/ && \
    rm /tmp/gradle-${GRADLE_VERSION}-bin.zip && \
    mv /usr/local/gradle-${GRADLE_VERSION} /usr/local/gradle && \
    ln -sf /usr/local/gradle/bin/gradle /usr/local/bin/gradle

COPY ./.s2i/bin /usr/local/s2i
RUN chmod a+x /usr/local/s2i/run /usr/local/s2i/assemble

LABEL io.openshift.s2i.scripts-url=image:///usr/local/s2i

RUN mkdir /wks && chown -R 1001:0 /wks

VOLUME /wks

USER 1001
EXPOSE 8080
