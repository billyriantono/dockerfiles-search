FROM maven:3.5.2-jdk-8

# Environment variables to configure custom maven repository.
ENV ARTIFACTORY_USERNAME=
ENV ARTIFACTORY_PASSWORD=
ENV ARTIFACTORY_CONTEXT_URL=https://jcenter.bintray.com

# Set default timzone to Amsterdam.
ENV TZ=Europe/Amsterdam

# Install nodeJs 
RUN export APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn &&\
    wget --quiet -O - https://deb.nodesource.com/setup_10.x | bash - &&\
    apt-get install -y nodejs   

# Install Ruby
RUN apt-get update && apt-get install -y ruby-full

# Install Sencha Cmd
RUN wget -nv -O SenchaCmd.zip \
      http://cdn.sencha.com/cmd/6.5.2/no-jre/SenchaCmd-6.5.2-linux-amd64.sh.zip  &&\
    unzip SenchaCmd.zip &&\
    $(find . -type f -name SenchaCmd-*-linux-amd64.sh) -q -Dall=true &&\
    rm SenchaCmd*

ENV LOCAL_CACHE_REPO=/local-cache-repo
ENV MAVEN_OPTS="-Xms256m -Xmx2048m"

# Configure default maven repositories
COPY settings.xml $MAVEN_CONFIG/settings.xml

# Warm up cache with Alfresco SDK's
COPY warmup-cache.sh warmup-cache.sh
RUN ./warmup-cache.sh

# Configure entry point 
COPY dev-entrypoint.sh /usr/local/bin/dev-entrypoint.sh
ENTRYPOINT ["/usr/local/bin/dev-entrypoint.sh"]
CMD ["mvn"]
