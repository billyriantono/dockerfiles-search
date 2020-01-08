FROM alpine:3.10 as builder

RUN mkdir -p /maven && wget http://mirrors.ircam.fr/pub/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz -O maven.tar.gz \
    && cat maven.tar.gz | tar xzf - -C /maven --strip-components 1 && rm -f maven.tar.gz

FROM openjdk:14-jdk-oracle

COPY --from=builder /maven /maven

ENV MAVEN_HOME=/maven PATH=/maven/bin:${PATH}
