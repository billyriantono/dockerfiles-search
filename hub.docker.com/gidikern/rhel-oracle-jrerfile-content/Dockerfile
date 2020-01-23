FROM java:8-jre-alpine

RUN apk add --update bash libstdc++ && rm -rf /var/cache/apk/*

WORKDIR /opt
ADD https://services.gradle.org/distributions/gradle-2.14.1-bin.zip .
RUN unzip gradle-2.14.1-bin.zip
ENV PATH="${PATH}:/opt/gradle-2.14.1/bin"

CMD gradle -version
