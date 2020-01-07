FROM mysql:5.6

RUN apt-get update && \
    apt-get install -y \
      netcat-openbsd

ADD readinessprobe /usr/local/bin/readinessprobe
