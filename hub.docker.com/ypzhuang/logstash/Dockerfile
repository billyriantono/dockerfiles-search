FROM logstash:2.4

MAINTAINER ypzhuang <zhuangyinping@gmail.com>

RUN mkdir /config/

COPY logstash.conf /config/

CMD ["-f", "/config/logstash.conf"]
