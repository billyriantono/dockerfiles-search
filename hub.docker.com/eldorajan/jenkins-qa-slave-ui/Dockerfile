FROM openjdk:8-jdk-alpine

RUN apk upgrade --update

RUN apk add --no-cache bash
RUN apk add --no-cache wget
RUN apk add --no-cache curl

RUN apk --no-cache add ca-certificates
RUN echo -e "http://nl.alpinelinux.org/alpine/v3.9/main\nhttp://nl.alpinelinux.org/alpine/v3.9/community" > /etc/apk/repositories

RUN apk add --no-cache git

RUN apk add --no-cache maven

RUN apk add --no-cache firefox-esr
RUN apk add --no-cache chromium
RUN apk add --no-cache chromium-chromedriver

COPY ./geckodriver /usr/local/bin/
RUN chmod a+x /usr/local/bin/geckodriver

COPY ./chromedriver /usr/local/bin/
RUN chmod a+x /usr/local/bin/chromedriver

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
ENV M2_HOME /usr/share/maven
ENV CHROME_BIN /usr/bin/chromium-browser

RUN export JAVA_HOME
RUN export M2_HOME
RUN export CHROME_BIN

CMD ["cat"]
