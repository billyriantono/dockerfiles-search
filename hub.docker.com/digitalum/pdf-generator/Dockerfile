FROM openjdk:8-jdk-alpine as build
WORKDIR /workspace/app

COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src

RUN ./mvnw install -DskipTests






FROM ubuntu:18.04
WORKDIR /app

RUN apt-get update
RUN apt-get install --yes curl
RUN curl --silent --location https://deb.nodesource.com/setup_4.x
RUN apt-get install --yes nodejs
RUN apt-get install --yes build-essential
RUN apt-get install --yes npm
RUN apt-get install --assume-yes chromium-browser
RUN npm install -g pm2


RUN apt-get update -y                             && \
    apt-get install software-properties-common -y && \
    add-apt-repository  ppa:openjdk-r/ppa -y    && \
    apt-get update -y                             && \
    apt-get install openjdk-8-jdk -y

RUN mkdir /opt/temp
ARG DEPENDENCY=/workspace/app/target
COPY --from=build ${DEPENDENCY}/*jar /opt/app.jar
COPY src/main/resources/application.properties /opt/application.properties


CMD pm2 start chromium-browser  --interpreter none -- --headless  --disable-gpu   --disable-translate   --disable-extensions   --disable-background-networking   --safebrowsing-disable-auto-update   --disable-sync   --metrics-recording-only   --disable-default-apps   --no-first-run   --mute-audio   --hide-scrollbars --disable-features=NetworkService --no-sandbox --remote-debugging-port=9223 --disable-dev-shm-usage --enable-logging=stderr --v=1  --user-data-dir=/app && java -jar /opt/app.jar


####FROM openjdk:8-jdk-alpine
####
####
####
####
####ARG BUILD_DATE
####ARG VCS_REF
####
####LABEL org.label-schema.build-date=$BUILD_DATE \
####      org.label-schema.description="Chrome running in headless mode in a tiny Alpine image" \
####      org.label-schema.name="alpine-chrome" \
####      org.label-schema.schema-version="1.0.0-rc1" \
####      org.label-schema.usage="https://github.com/Zenika/alpine-chrome/blob/master/README.md" \
####      org.label-schema.vcs-url="https://github.com/Zenika/alpine-chrome" \
####      org.label-schema.vcs-ref=$VCS_REF \
####      org.label-schema.vendor="Zenika" \
####      org.label-schema.version="latest"
####
##### Installs latest Chromium package.
####RUN echo @edge http://nl.alpinelinux.org/alpine/edge/community > /etc/apk/repositories \
####    && echo @edge http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories \
####    && apk add --no-cache \
####    libstdc++@edge \
####    chromium@edge \
####    harfbuzz@edge \
####    nss@edge \
####    freetype@edge \
####    ttf-freefont@edge \
####    && rm -rf /var/cache/* \
####    && mkdir /var/cache/apk
####
##### Add Chrome as a user
####RUN mkdir -p /usr/src/app \
####    && adduser -D chrome \
####    && chown -R chrome:chrome /usr/src/app
##### Run Chrome as non-privileged
####USER chrome
####WORKDIR /usr/src/app
####
####ENV CHROME_BIN=/usr/bin/chromium-browser \
####    CHROME_PATH=/usr/lib/chromium/
####
####
####
####
####VOLUME /tmp1
#####ARG JAR_FILE
#####COPY ${JAR_FILE} app.jar
####COPY target/pdf-request-engine-0.0.1-SNAPSHOT.jar /opt/app.jar
####COPY src/main/resources/application.properties /opt/application.properties
#####ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
####
####
####
#####CMD  java -jar /opt/app.jar
####ENTRYPOINT ["chromium-browser", "--no-sandbox", "--headless", "--disable-gpu", "--disable-software-rasterizer", "--disable-dev-shm-usage"]
####
####EXPOSE 8081
####
####