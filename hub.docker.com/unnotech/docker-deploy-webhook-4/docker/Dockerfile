from jboss/keycloak-postgres

ADD standalone.xml keycloak/standalone/configuration/standalone.xml
ADD ulock-theme.zip ulock-theme.zip
RUN keycloak/bin/jboss-cli.sh --command="module add --name=co.ulock.theme --resources=ulock-theme.zip"
