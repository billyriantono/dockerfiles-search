# Stage 1 (build project)
FROM openjdk:12-alpine AS builder

LABEL maintainer="Raphael Medeiros <raphael.medeiros@gmail.com>"

RUN mkdir -p /usr/src/liten/
WORKDIR /usr/src/liten/
RUN apk --no-cache add git maven
RUN git clone -b master https://github.com/byraphaelmedeiros/liten.git .
RUN mvn package -Dmaven.test.skip=true

# Stage 2 (build image)
FROM openjdk:12-alpine

LABEL maintainer="Raphael Medeiros <raphael.medeiros@gmail.com>"

ENV MONGODB_URI="mongodb://localhost/liten"

RUN apk update \
 && apk add --update ca-certificates \
 && apk add --update -t deps curl \
 && apk add --no-cache bash gawk sed grep bc coreutils vim wget curl tar tzdata \
 && apk del --purge deps \
 && rm /var/cache/apk/*

RUN cp /usr/share/zoneinfo/America/Fortaleza /etc/localtime

ENV LANG=pt_BR.UTF-8 \
    LANGUAGE=pt_BR:pt \
    LC_ALL=pt_BR.UTF-8

WORKDIR /
COPY --from=builder /usr/src/liten/liten-web/target/liten-web.jar /app.jar

EXPOSE 8080

ENTRYPOINT ["java", "--add-opens", "java.base/java.lang=ALL-UNNAMED", "-Djava.security.egd=file:/dev/./urandom", "-Dfile.encoding=UTF-8", "-Xms256m", "-Xmx512m", "-jar", "/app.jar"]