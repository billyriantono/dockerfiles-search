FROM alpine:edge

RUN apk add --update git lua-dev gcc make openssl-dev pcre-dev g++ 

WORKDIR /root

RUN git clone https://github.com/lefcha/imapfilter.git

WORKDIR /root/imapfilter

RUN make all
RUN make install
RUN mkdir /root/.imapfilter


COPY crontab /var/spool/cron/crontabs/root
CMD imapfilter




VOLUME /root/.imapfilter
CMD ["crond", "-f", "-l", "0", "-d", "0"]
