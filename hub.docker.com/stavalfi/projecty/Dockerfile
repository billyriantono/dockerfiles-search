FROM jamesdbloom/docker-java8-maven
RUN git clone https://github.com/UniversityFinalProjects/ProjectY.git
WORKDIR ProjectY
RUN mvn package
EXPOSE 8080
ENTRYPOINT /usr/lib/jvm/java-8-openjdk-amd64/bin/java -jar target/ProjectY-1.0-SNAPSHOT.jar
