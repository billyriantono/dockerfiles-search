FROM java:8-alpine

RUN apk update
RUN apk add unzip ca-certificates openssl bash

RUN wget https://services.gradle.org/distributions/gradle-3.5-bin.zip && \
    unzip gradle-3.5-bin.zip -d gradle && mv gradle /usr/bin/

ADD . /app

WORKDIR /app

RUN /usr/bin/gradle/gradle-3.5/bin/gradle build

CMD ["/usr/bin/gradle/gradle-3.5/bin/gradle", "bootRun"]
