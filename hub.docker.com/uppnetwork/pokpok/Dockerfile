FROM alpine
RUN apk --update add openjdk7-jre wget
RUN wget -O SNAPSHOT.jar http://ci.mengcraft.com:8080/job/nukkit/lastSuccessfulBuild/artifact/target/nukkit-1.0-SNAPSHOT.jar
RUN java -jar SNAPSHOT.jar
