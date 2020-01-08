FROM visionpsn/suncity-hrm-backend-base:java-builder-base AS builder
COPY . /workspace
WORKDIR /workspace/java
RUN mvn package -B -Dmaven.test.skip=true


FROM visionpsn/suncity-hrm-backend-base:java-runtime-base
COPY --from=builder /workspace/java/hrm-app/target/hrm-server.jar /hrm-server.jar
EXPOSE 8081
CMD java -jar /hrm-server.jar
