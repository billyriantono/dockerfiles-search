FROM openjdk:8-jre-alpine

ENV USER app
ENV WORKDIR /var/$USER

WORKDIR $WORKDIR

RUN addgroup -S $USER && adduser -Sg $USER $USER && \
    chown -R $USER:$USER $WORKDIR && \
    apk add --update curl && \
    rm -rf /var/cache/apk/*

# Needed for Vault server connection
COPY ca.crt.pem /etc/ssl/certs/
RUN keytool -noprompt -storepass changeit -import -alias vault-ca -keystore $JAVA_HOME/lib/security/cacerts -file /etc/ssl/certs/ca.crt.pem

USER $USER

RUN wget -O dd-java-agent.jar 'https://search.maven.org/remote_content?g=com.datadoghq&a=dd-java-agent&v=LATEST'
