FROM maven:3-jdk-8
WORKDIR /home/app
COPY . $WORKDIR
RUN mvn install
CMD java -jar Hello-1.0-SNAPSHOT.jar