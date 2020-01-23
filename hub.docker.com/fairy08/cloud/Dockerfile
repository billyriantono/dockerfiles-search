FROM golang as go
COPY scripts/suid/main_linux.go /tmp/suid/main.go
WORKDIR /tmp/suid
RUN go build -o please

#FROM  maven as pack
#WORKDIR /tmp/app
#COPY pom.xml /tmp/app/pom.xml
#RUN mvn dependency:resolve
#COPY . /tmp/app/
#RUN mvn package

FROM debian:buster as base-system
COPY scripts/sources.list /etc/apt/sources.list
COPY scripts/prepare.sh /tmp/prepare.sh
RUN /bin/bash -v -e /tmp/prepare.sh
COPY scripts/espeed.sql /tmp/espeed.sql
COPY scripts/truncate.sql /tmp/truncate.sql
COPY scripts/create.sh /tmp/create.sh
COPY scripts/supervisord.conf /tmp/supervisord.conf
RUN /bin/bash -v -e /tmp/create.sh

FROM base-system as production
COPY --from=go /tmp/suid/please /usr/bin/please
#COPY --from=pack /tmp/app/target/cloud-*.jar /var/www/cloud.jar
COPY scripts/cloud.jar /var/www/cloud.jar
RUN /bin/chmod 4755 /usr/bin/please

EXPOSE 8888 4600
ENTRYPOINT ["supervisord","-c","/etc/supervisor/supervisord.conf"]
