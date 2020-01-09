FROM pandeiro/oracle-jdk8
MAINTAINER Bamdad Dashtban

WORKDIR /usr/bin
RUN apt-get install -y unzip
RUN wget https://services.gradle.org/distributions/gradle-2.4-all.zip && \
    unzip gradle-2.4-all.zip && \
    ln -s gradle-2.4 gradle && \
    rm gradle-2.4-all.zip

ENV GRADLE_HOME /usr/bin/gradle
ENV PATH $PATH:$GRADLE_HOME/bin

# Default command is "/usr/bin/gradle -version" on /app dir
# (ie. Mount project at /app "docker --rm -v /path/to/app:/app gradle <command>")
RUN mkdir /app
WORKDIR /app

