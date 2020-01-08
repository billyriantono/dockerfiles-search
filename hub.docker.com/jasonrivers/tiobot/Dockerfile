FROM java:8-alpine as builder

ADD . /TIOBot-src

RUN mkdir /config

RUN cd /TIOBot-src && \
    sh ./gradlew shadowJar

FROM java:8-alpine

RUN adduser -D -h /TIOBot -u 1000 tiobot

USER tiobot

COPY --from=builder /TIOBot-src/build/libs/TIOExchange-*-shadow.jar /TIOBot/TIOBot.jar

VOLUME /TIOBot/config

WORKDIR /TIOBot

CMD java -jar /TIOBot/TIOBot.jar /TIOBot/config/
