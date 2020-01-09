FROM ubuntu:18.04

ADD mail.txt .
RUN apt-get update && \
    apt-get install -y \
      mailutils \
      && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN service postfix start

CMD ["sh", "send.sh"]