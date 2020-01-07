FROM ubuntu:latest

USER root

RUN apt-get update \
    && apt-get install -y openjdk-8-jdk curl wget unzip xvfb chromium-browser chromium-chromedriver \
    && rm -rf /var/lib/apt/lists/*

#
# Maven install
#

ARG MAVEN_VERSION=3.6.0
ARG USER_HOME_DIR="/root"

RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && wget -q -O - http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
    | tar -xzC /usr/share/maven --strip-components=1 \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

RUN curl -SsL https://downloads.gauge.org/stable | sh

ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

#
# Gauge install
#

RUN curl -SL https://github.com/getgauge/gauge-java/archive/master.zip -o master.zip \
     && unzip -q master.zip && rm master.zip \
     && mvn -Dmaven.test.skip=true -Dgpg.skip=true  -f gauge-java-master install \
    && rm -rf gauge-java-master

RUN gauge telemetry off


#
# Startup files
#

COPY entrypoint.sh /opt/bin/entrypoint.sh
RUN chmod +x /opt/bin/entrypoint.sh

COPY project.example /project.example
WORKDIR /project.example
RUN mvn -B test || mvn -B clean && rm -rf .gauge && mkdir /project
WORKDIR /project 
VOLUME "$USER_HOME_DIR/.m2"

# EXPOSE 4444
ENV GEOMETRY 1024x768x16
ENTRYPOINT ["/opt/bin/entrypoint.sh"]
CMD ["mvn", "clean", "test"]

