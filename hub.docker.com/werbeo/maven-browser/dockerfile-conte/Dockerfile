FROM openjdk:8-jdk-alpine

MAINTAINER Bertrand Mandrin <bertrandmandrin@gmail.com>

ENV HAWKBIT_VERSION=0.3.0M5 \
    HAWKBIT_HOME=/opt/hawkbit \
    JAR_FILE=hawkbit-update-server.jar

EXPOSE 8080

######### General install
RUN set -x \
    && apk add --no-cache gnupg unzip \
    && apk add --no-cache libressl wget \
    && apk add --no-cache git maven python2

RUN mkdir -p $HAWKBIT_HOME \
    && cd $HAWKBIT_HOME

######### Hawkbit
RUN git clone https://github.com/eclipse/hawkbit.git -b $HAWKBIT_VERSION

######### Add mysql dependency
COPY add_mysql.py /hawkbit/hawkbit-repository/hawkbit-repository-jpa/add_mysql.py
RUN cd /hawkbit/hawkbit-repository/hawkbit-repository-jpa/ \
    && ./add_mysql.py \
    && cd -

######### Add mariadb dependency in Hawkbit
COPY 0001-Add-mariadb-dependency.patch /hawkbit/
RUN cd /hawkbit/ \
    && dos2unix 0001-Add-mariadb-dependency.patch \
    && git apply --ignore-whitespace 0001-Add-mariadb-dependency.patch \
    && cd -

RUN cd hawkbit \
    && mvn install

RUN cp /hawkbit/hawkbit-runtime/hawkbit-update-server/target/hawkbit-update-server-0.3.0-SNAPSHOT.jar $HAWKBIT_HOME/hawkbit-update-server.jar

VOLUME "$HAWKBIT_HOME/data"

COPY application.properties $HAWKBIT_HOME

COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

WORKDIR $HAWKBIT_HOME

ENTRYPOINT ["/entrypoint.sh"]
