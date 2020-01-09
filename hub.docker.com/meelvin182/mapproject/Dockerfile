FROM openjdk:8-jdk-alpine
VOLUME /var
WORKDIR /workspace/app
COPY src src
COPY gradlew .
COPY gradle gradle
COPY build.gradle .
COPY settings.gradle .
RUN chmod +x gradlew && ./gradlew clean
RUN ./gradlew build -x test
RUN ls -ltr
CMD java -jar build/libs/*.jar
EXPOSE 9999