FROM anapsix/alpine-java

ADD ./*.sh /tmp/kafka/

WORKDIR /tmp/kafka

RUN sh install.sh

EXPOSE 2181 9092

CMD ["sh", "start.sh"]
