#docker run -ti --entrypoint /bin/sh YOUR_IMAGE
#docker run -ti --entrypoint /bin/sh YOUR_IMAGE
FROM eduardoborgono2/ubuntu-java-git:1

RUN git clone https://github.com/eduborgono/Microservices-TPS.git

WORKDIR /Microservices-TPS/recomendador

RUN chmod +x gradlew
RUN ./gradlew && ./gradlew build

WORKDIR /app

RUN mv /Microservices-TPS/recomendador/build/libs/recomendador-all.jar .
RUN rm -rf /Microservices-TPS

EXPOSE 8080

CMD ["java", "-jar", "recomendador-all.jar"]