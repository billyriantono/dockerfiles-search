FROM sgrio/java-oracle:server_jre_8
MAINTAINER Florian Esser <fe@wetransform.to>

USER root
COPY resources/imported-certs $JAVA_HOME/jre/lib/security/imported-certs
COPY resources/import-certs $JAVA_HOME/jre/lib/security
RUN \
    cd $JAVA_HOME/jre/lib/security \
	&& ./import-certs
