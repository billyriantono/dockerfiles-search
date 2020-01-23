FROM openjdk:8-jdk

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install nodejs
RUN mkdir -p /project
ADD https://downloads.typesafe.com/typesafe-activator/1.3.12/typesafe-activator-1.3.12-minimal.zip /root/play.zip
RUN unzip /root/play.zip -d /root && chmod +x /root/activator-1.3.12-minimal/bin/activator \
    && rm /root/play.zip

ENV PATH /root/activator-1.3.12-minimal/bin:$PATH
ENV ACTIVATOR_HOME /root/activator-1.3.12-minimal/bin

VOLUME /project
WORKDIR /project

EXPOSE 9000 9999

ENV health_check_url=http://localhost:9000/api/doc

HEALTHCHECK --interval=30s --timeout=30s --start-period=30s --retries=5 CMD curl -f ${health_check_url} || exit 1

ENTRYPOINT [ "activator", "clean", "compile", "run", "-jvm-debug", "9999" ]