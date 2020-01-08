FROM maven:3.6.0-jdk-11-slim

ADD maven/setup/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

#ADD maven/setup/installDocker.sh /installDocker.sh
#RUN chmod +x /installDocker.sh
#RUN ./installDocker.sh

WORKDIR /project

VOLUME ["/project", "/repository"]
ENTRYPOINT ["/entrypoint.sh"]
CMD ["mvn", "verify"]
