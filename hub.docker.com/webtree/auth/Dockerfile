# Build
FROM webtree/build-images:maven-jdk-8 as builder

RUN mkdir /build
WORKDIR /build
COPY . .
RUN mvn package -Dmaven.test.skip=true

# Main
FROM openjdk:8-slim
COPY --from=builder /build/auth-core/target/auth-core-*-SNAPSHOT.jar /app.jar
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom","-jar", "/app.jar"]
