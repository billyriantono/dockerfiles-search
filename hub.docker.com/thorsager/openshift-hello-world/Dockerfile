FROM maven:3-jdk-10-slim as builder

RUN useradd -u 10000 thorsager
RUN mkdir /build && chown thorsager /build
USER thorsager

WORKDIR /build
COPY pom.xml /build/

RUN mvn -B -Dmaven.repo.local=/build/.m2/repository dependency:go-offline

COPY src /build/src

RUN mvn -B -Dmaven.repo.local=/build/.m2/repository package

FROM openjdk:10-jre

RUN useradd -u 10000 thorsager
USER thorsager
COPY --from=builder /build/target/*.jar /app.jar

CMD ["java","-jar", "/app.jar"]
