FROM maven as builder

COPY . .

RUN mvn clean install

FROM openjdk:11-slim

COPY --from=builder /facebook-velobot-web/target .

CMD java -jar tombot.jar

EXPOSE 80