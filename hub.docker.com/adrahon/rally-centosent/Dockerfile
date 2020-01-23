FROM thaiphamquoc/docker-java:0.10.2
LABEL maintainer="thaiphamquoc@gmail.com"

ENV DEBUGGER_PORT=8998
ENV JAVA_DEBUGGER_OPTION="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=${DEBUGGER_PORT}"

COPY etc/services.d/java/run /etc/services.d/java/
RUN chmod +x /etc/services.d/java/run
RUN ln -s /target/application.jar /application.jar

EXPOSE ${DEBUGGER_PORT}
