FROM openjdk:8 AS build
LABEL description="Build environment for sample application"
WORKDIR /tmp
RUN git clone https://github.com/gnu-gnu/prj4devops.git
WORKDIR /tmp/prj4devops
RUN git checkout multi-stage
RUN chmod u+x mvnw
RUN ./mvnw clean package

FROM openjdk:8
LABEL description="Running environment for sample application"
COPY --from=build /tmp/prj4devops/target/demo-0.0.1-SNAPSHOT.jar /tmp/demo.jar
EXPOSE 18080
WORKDIR /tmp
ENTRYPOINT [ "java", "-jar", "demo.jar" ]