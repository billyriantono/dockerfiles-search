FROM jboss/keycloak:4.8.2.Final

ADD docker-entrypoint.sh /opt/jboss/

EXPOSE 8080

ENTRYPOINT [ "/opt/jboss/docker-entrypoint.sh" ]

CMD ["-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-Djboss.socket.binding.port-offset=100"]