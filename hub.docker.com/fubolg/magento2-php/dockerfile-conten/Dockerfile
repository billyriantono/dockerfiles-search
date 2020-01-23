FROM java:8-alpine

ENV DEX2JAR_VERSION 2.0

RUN apk update && \
    apk add --no-cache --virtual .build-deps wget unzip && \
    wget https://nchc.dl.sourceforge.net/project/dex2jar/dex2jar-${DEX2JAR_VERSION}.zip -O /tmp/dex2jar-${DEX2JAR_VERSION}.zip && \
    unzip /tmp/dex2jar-${DEX2JAR_VERSION}.zip -d /tmp/ && \
    mv /tmp/dex2jar-${DEX2JAR_VERSION}/* /usr/local/bin/ && \
    chmod a+x /usr/local/bin/*.sh && \
    apk del .build-deps && \
    rm -rf /root/.cache && rm -rf /var/cache/apk/*