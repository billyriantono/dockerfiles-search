FROM maven:3.6.0-jdk-7-alpine

# speed up Maven
ENV MAVEN_OPTS="-XX:+TieredCompilation -XX:TieredStopAtLevel=1 -Dmaven.repo.local=source/.caches/mvn"
ENTRYPOINT ["/usr/bin/mvn"]

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

CMD ["-f", "source/pom.xml", "-s", "source/mvn.settings.xml", "clean", "install"]
