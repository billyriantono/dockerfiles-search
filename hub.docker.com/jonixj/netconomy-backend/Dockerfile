FROM maven:3
WORKDIR /app
ADD . ./
RUN mvn install
CMD ["java","-Djava.security.egd=file:/dev/./urandom","-Dspring.profiles.active=${profile:production}","-jar","target/netconomy-0.1.0-SNAPSHOT.jar"]
