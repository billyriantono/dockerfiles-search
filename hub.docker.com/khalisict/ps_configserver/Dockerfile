FROM openjdk:8-alpine
VOLUME /tmp
ARG DEPENDENCY=target
COPY ${DEPENDENCY}/classes/known_hosts /pssln/ssh/known_hosts
COPY ${DEPENDENCY}/ps_configserver-0.0.1.jar /pssln/app/ps_configserver-0.0.1.jar
ENTRYPOINT ["java","-jar","/pssln/app/ps_configserver-0.0.1.jar"]