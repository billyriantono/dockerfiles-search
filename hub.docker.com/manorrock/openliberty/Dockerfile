FROM manorrock/openjdk:11.0.3
ENV OPENLIBERTY_VERSION=19.0.0.10
RUN apt-get update && \
    apt-get install -y curl unzip && \
    cd /usr/local && \
    curl -O https://public.dhe.ibm.com/ibmdl/export/pub/software/openliberty/runtime/release/2019-10-02_0300/openliberty-javaee8-19.0.0.10.zip && \
    unzip openliberty-javaee8-19.0.0.10.zip && \
    mv wlp openliberty$OPENLIBERTY_VERSION && \
    rm openliberty-javaee8-19.0.0.10.zip && \
    rm -rf /var/lib/apt/lists/* && \
    /usr/local/openliberty$OPENLIBERTY_VERSION/bin/server create defaultServer
CMD /usr/local/openliberty$OPENLIBERTY_VERSION/bin/server run defaultServer 
EXPOSE 8080
WORKDIR /mnt

