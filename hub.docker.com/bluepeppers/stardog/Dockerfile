FROM dockerfile/java:oracle-java7

ENV STARDOG_VER stardog-2.2.4
ENV STARDOG_URL http://stardog.s3-website-us-east-1.amazonaws.com/downloads/bebcc209-17fd-4494-bfaf-b18e5bfa2640/${STARDOG_VER}.zip
ENV STARDOG_HOME /stardog

WORKDIR /

RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup && \
    echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache && \
    apt-get update && apt-get update -yy && \
    mkdir -p $STARDOG_HOME && \
    apt-get install -yy wget unzip && \
    wget $STARDOG_URL && \
    unzip ${STARDOG_VER}.zip && \
    rm ${STARDOG_VER}.zip && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /${STARDOG_VER}

EXPOSE 5820

CMD wget -O $STARDOG_HOME/stardog-license-key.bin $STARDOG_LICENSE && \
    ./bin/stardog-admin server start && \
    sleep 1 && \
    (tail -f $STARDOG_HOME/stardog.log &) && \
    while (pidof java > /dev/null); do sleep 1; done
