FROM maven:latest

COPY massim/ root/

WORKDIR root/

RUN mvn install

WORKDIR server/

EXPOSE 8000

CMD mvn exec:java -Dexec.args="--monitor"