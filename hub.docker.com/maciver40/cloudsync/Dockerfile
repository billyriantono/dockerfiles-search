FROM maciver40/ubuntu-base

LABEL maintainer="robert@eisenmann.email"

EXPOSE 14443

RUN \
    wget -O - https://repo.jotta.us/public.gpg | apt-key add - && \
    echo "deb https://repo.jotta.us/debian debian main" | tee /etc/apt/sources.list.d/jotta-cli.list && \
    apt-get update && apt-get install -y jotta-cli && \
    cp /etc/jottad/config.ini.bak /etc/jottad/config.ini
    
VOLUME ["/config"]
VOLUME ["/mnt/user/backup"]
