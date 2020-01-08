FROM maven:3.6.0-jdk-11-slim
VOLUME /tmp

COPY . /app

WORKDIR /app
RUN mvn -B -s /usr/share/maven/ref/settings-docker.xml install
RUN rm -rf /app/*