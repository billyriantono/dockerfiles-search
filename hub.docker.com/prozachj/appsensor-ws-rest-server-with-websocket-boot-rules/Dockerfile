FROM prozachj/appsensor-build

COPY . appsensor-ws-rest-server-with-websocket-boot-rules
WORKDIR appsensor-ws-rest-server-with-websocket-boot-rules
RUN mvn install && mvn test && mvn package
ENV APPSENSOR_WEB_SOCKET_HOST_URL=ws://localhost:8085/dashboard
CMD ["java","-Djava.security.egd=file:/dev/./urandom","-jar","target/appsensor-ws-rest-server-with-websocket-boot-rules-0.0.1-SNAPSHOT.jar"]
EXPOSE 8085
