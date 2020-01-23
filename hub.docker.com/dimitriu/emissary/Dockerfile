FROM gradle:jdk11 AS build
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle build --no-daemon
RUN jlink \
    --compress=2 \
    --module-path /usr/lib/jvm/default-jvm/jmods \
    --add-modules java.base,java.logging,java.xml,jdk.unsupported,java.sql,java.naming,java.desktop,java.management,java.security.jgss,java.instrument \
    --output /jdk-minimal


FROM openjdk:13-alpine
ENV APP_ROOT /app
RUN mkdir ${APP_ROOT} /jdk

COPY --from=build /home/gradle/src/build/libs/*.jar ${APP_ROOT}/run.jar
COPY --from=build /jdk-minimal/* /jdk/
WORKDIR ${APP_ROOT}
ENTRYPOINT ["/jdk/bin/java", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-Djava.security.egd=file:/dev/./urandom", "-jar", "run.jar"]
