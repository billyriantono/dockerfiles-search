FROM openjdk:11-jdk-stretch

RUN apt-get update && apt-get install -y unzip git wget


RUN mkdir -p /maven
RUN wget --quiet http://mirrors.ircam.fr/pub/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz -O maven.tar.gz \
    && cat maven.tar.gz | tar xzf - -C /maven --strip-components 1 && rm -f maven.tar.gz

ENV MAVEN_HOME=/maven
ENV PATH=/maven/bin:${PATH}
