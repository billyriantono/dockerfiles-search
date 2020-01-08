FROM java:8

ADD ./*.sh /tmp/kafka/

WORKDIR /tmp/kafka

RUN sh build.sh

EXPOSE 2181 9092

CMD ["sh", "start.sh"]
