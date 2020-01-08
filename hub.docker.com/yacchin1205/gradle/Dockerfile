FROM java:7

ADD https://services.gradle.org/distributions/gradle-2.14-bin.zip \
    /tmp/gradle-bin.zip
RUN cd /opt/; unzip /tmp/gradle-bin.zip

ENV PATH=$PATH:/opt/gradle-2.14/bin/

