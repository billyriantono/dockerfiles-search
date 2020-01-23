FROM ubuntu:18.04
COPY . .
RUN apt-get update && apt-get install -y \
    openjdk-8-jdk \
&& rm -rf /var/lib/apt/lists/*
RUN chmod +x ./gradlew && ./gradlew build
CMD ["java", "-jar", "cicd.jar"]