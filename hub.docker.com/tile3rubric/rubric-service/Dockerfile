FROM gradle:5.6.2-jdk11 as build
WORKDIR /workspace/app

COPY . .
RUN gradle clean build
RUN ls -lah build/libs
RUN mkdir -p target/dependency && (cd target/dependency; jar -xf ../../build/libs/*.jar)

FROM adoptopenjdk/openjdk11:latest
VOLUME /tmp
ARG DEPENDENCY=/workspace/app/target/dependency
COPY --from=build ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY --from=build ${DEPENDENCY}/META-INF /app/META-INF
COPY --from=build ${DEPENDENCY}/BOOT-INF/classes /app
ENTRYPOINT ["java","-cp","/app:/app/lib/*","be.hogent.tile3.rubricservice.RubricServiceApplication"]
