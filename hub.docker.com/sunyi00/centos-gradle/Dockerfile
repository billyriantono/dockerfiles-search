FROM sunyi00/centos-java:1.0.0

ENV DOWNLOAD_URL https://services.gradle.org/distributions/gradle-2.8-bin.zip

RUN yum install -y wget curl tar unzip \
    && mkdir -p /opt/ \
    && cd /opt/ \
    && wget $DOWNLOAD_URL \
    && unzip gradle-*.zip \
    && rm -f gradle-*.zip \
    && mv gradle-* gradle \
    && echo 'export GRADLE_HOME=/opt/gradle' >> /etc/profile \
    && echo 'export PATH=$GRADLE_HOME/bin:$PATH' >> /etc/profile

ENV GRADLE_HOME /opt/gradle
ENV PATH $GRADLE_HOME/bin:$PATH
