FROM ruby:2.3

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y nodejs --no-install-recommends && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y mysql-client postgresql-client sqlite3 --no-install-recommends && rm -rf /var/lib/apt/lists/*

COPY run.sh /run.sh
RUN chmod u+rwx /run.sh

EXPOSE 3000

ENTRYPOINT [ "/run.sh" ]
