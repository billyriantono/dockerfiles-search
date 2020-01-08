FROM openjdk:11-jre-slim
COPY . /usr/local/lib/
WORKDIR /usr/local/lib
EXPOSE 25565
ENTRYPOINT ["java","-Xmx1024M","-Xms1024M","-jar","/usr/local/lib/spigot-1.12.2.jar"]

# Build & RUN
# docker build -f webgenerator.docker -t webgenerator:il_mio_wg_personalizzato .
# docker run -it --rm -d -p 8085:8085 webgenerator:il_mio_wg_personalizzato