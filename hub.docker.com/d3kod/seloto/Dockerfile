FROM maven:3-jdk-8

COPY . /build/
WORKDIR /build
RUN mvn package && \
    mkdir /share/ && \
    cp target/seloto-website*.war /share/seloto-website.war
VOLUME /share/

CMD /bin/sh -c '/bin/echo "Seloto Website WAR file available in /share"'
