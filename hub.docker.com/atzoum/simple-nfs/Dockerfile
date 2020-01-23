FROM maven:3.5-jdk-8 as builder
RUN apt-get update && apt-get -y install git && \
    git clone https://github.com/kofemann/simple-nfs.git && \
    cd simple-nfs && \
    mvn clean package

FROM openjdk:8-slim
COPY --from=builder /simple-nfs/target/simple-nfs-1.0-SNAPSHOT-jar-with-dependencies.jar /usr/src/simple-nfs/simple-nfs.jar
WORKDIR /usr/src/simple-nfs
ENTRYPOINT java -jar simple-nfs.jar
CMD ["-with-portmap","-root","/","-exportsFile","/etc/exports"]
