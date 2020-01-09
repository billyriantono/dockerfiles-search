FROM maven:3-jdk-8

RUN apt-get update \
    && apt-get install -y mc vim nano curl tar gzip unzip telnet net-tools locales locales-all \
    && export LANGUAGE=ru_RU.UTF-8 \
    && export LC_ALL=ru_RU.UTF-8 \
    && export LANG=ru_RU.UTF-8 \
    && export LC_TYPE=ru_RU.UTF-8 \
    && sed -i -e "s/# ru_RU.UTF-8 UTF-8/ru_RU.UTF-8 UTF-8/" /etc/locale.gen \
    && echo 'LANG="$LANG"' > /etc/default/locale \
    && dpkg-reconfigure --frontend=noninteractive locales \
    && update-locale LANG=$LANG \
    #clean
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /opt/archive.tgz


COPY / /app/

WORKDIR /app/

RUN mvn package

EXPOSE 8080

CMD [ "/app/target/location-service-1.0-SNAPSHOT.jar"]
