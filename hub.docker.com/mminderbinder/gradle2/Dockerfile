# mminderbinder/gradle2:oracle-java8
# Gradle2 with Oracle Java 8 JDK Docker Image
FROM mminderbinder/java-jdk:oracle-java8
MAINTAINER Milo Minderbinder <minderbinder.enterprises@gmail.com>


RUN add-apt-repository ppa:cwchien/gradle
RUN apt-get update && apt-get -y install gradle-2.13

ENV GRADLE_PROJECTS_DIR /mnt/gradle-projects
ENV GRADLE_USER_HOME /mnt/.gradle
ENV MAVEN_USER_HOME /root/.m2

COPY gradle-build.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/gradle-build.sh

RUN mkdir -p $MAVEN_USER_HOME/repository

VOLUME $GRADLE_PROJECTS_DIR
VOLUME $GRADLE_USER_HOME
VOLUME $MAVEN_USER_HOME

WORKDIR $GRADLE_PROJECTS_DIR

# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/sbin/my_init", "--", "/usr/local/bin/gradle-build.sh"]
