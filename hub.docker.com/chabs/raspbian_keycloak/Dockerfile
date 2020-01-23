#FROM hypriot/rpi-java
FROM java

MAINTAINER Cédric CLOVEL

ADD https://downloads.jboss.org/keycloak/3.4.1.Final/keycloak-3.4.1.Final.tar.gz /opt/jboss/

ADD ./docker-entrypoint.sh /opt/jboss/

RUN cd /opt/jboss/ && \
    tar xzvf keycloak-3.4.1.Final.tar.gz && \
    rm -rf keycloak-3.4.1.Final.tar.gz && \
    mv keycloak-3.4.1.Final keycloak

EXPOSE 8080

ENTRYPOINT [ "/opt/jboss/docker-entrypoint.sh" ]

CMD ["-b", "0.0.0.0"]
