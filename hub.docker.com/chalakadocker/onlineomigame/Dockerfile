
FROM openjdk:8-jdk-alpine AS MAVEN_TOOL
# ----
# Install Maven
RUN apk add --no-cache curl tar bash
ARG MAVEN_VERSION=3.3.9
ARG USER_HOME_DIR="/root"
RUN mkdir -p /usr/share/maven && \
curl -fsSL http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar -xzC /usr/share/maven --strip-components=1 && \
ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"
# speed up Maven JVM a bit
ENV MAVEN_OPTS="-XX:+TieredCompilation -XX:TieredStopAtLevel=1"
ENTRYPOINT ["/usr/bin/mvn"]
# ----
# Install project dependencies and keep sources
# make source folder
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
# install maven dependency packages (keep in image)
COPY pom.xml /usr/src/app
# copy other source files (keep in image)
COPY src /usr/src/app/src
RUN mvn -T 1C clean install
#Doker running part
FROM tomcat:8.5.37-jre8

COPY --from=MAVEN_TOOL /usr/src/app/target/OnlineOmiGame-1.0-SNAPSHOT.war $CATALINA_HOME/webapps/OnlineOmiGame.war

#ENV JPDA_ADDRESS=8000
#ENV JPDA_TRANSPORT=dt_socket

EXPOSE 8080 8000
#CMD ["catalina.sh", "jpda", "run"]

CMD ["catalina.sh", "run"]