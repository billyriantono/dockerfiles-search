FROM ubuntu:bionic
LABEL maintainer="axemann@gmail.com"

ENV TROVE_CONFIG="/config"
ENV TROVE_DATA="/download"
ENV HB_API_KEY="Valid_Key_Required"
ENV HB_PLATFORM="windows"

RUN mkdir -p /$TROVE_CONFIG /$TROVE_DATA &&\
    apt-get update &&\
    apt-get install wget cron -y &&\
    rm -rf /var/lib/apt/lists/*

RUN wget https://gitlab.com/silver_rust/trove_downloader/-/jobs/artifacts/master/raw/target/x86_64-unknown-linux-musl/release/trove_downloader?job=x86_64-unknown-linux-musl -O /trove_downloader &&\
    chmod +x /trove_downloader

RUN echo "{\"api\":\"_simpleauth_sess=\\\"${HB_API_KEY}\\\"\",\"platform\":\"${HB_PLATFORM}\",\"location\":\"${TROVE_DATA}\"}" > ${TROVE_CONFIG}/config.json

ADD crontab /var/spool/cron/crontabs/root 
RUN chmod 0644 /var/spool/cron/crontabs/root

ADD setup_env /setup_env
RUN chmod 0755 /setup_env

VOLUME /config /download

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "/setup_env && service cron start && sleep 120 && /trove_downloader && /bin/bash" ]