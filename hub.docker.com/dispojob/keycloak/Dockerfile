FROM jboss/keycloak:4.0.0.Final

ENV DB_VENDOR MYSQL
ENV EXTRA_ARGS ""
ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_VERSION 3.3.9

USER root

ADD opt /opt

COPY --from=maven:3.3.9 /usr/share/maven /usr/share/maven

RUN ln -s /usr/share/maven/bin/mvn /usr/bin/mvn \
 && curl -fLS -o /opt/jboss/jbcrypt-0.4.jar http://central.maven.org/maven2/org/mindrot/jbcrypt/0.4/jbcrypt-0.4.jar \
 && chown -R jboss /opt/custom/symfony-users /opt/jboss

USER jboss

RUN /opt/jboss/keycloak/bin/jboss-cli.sh --command="module add --name=org.mindrot.jbcrypt --resources=jbcrypt-0.4.jar"
