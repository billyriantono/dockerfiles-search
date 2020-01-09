FROM library/ubuntu

WORKDIR /opt
ENV KAFKA=kafka_2.12-2.2.0
RUN apt-get update && apt-get install -y telnet iputils-ping net-tools curl iproute2 vim ucommon-utils netcat wget

RUN apt-get install -y mysql-client mongodb-clients postgresql-client

RUN apt-get install -y openjdk-11-jre
RUN wget https://www-us.apache.org/dist/kafka/2.2.0/${KAFKA}.tgz && tar zxvf ${KAFKA}.tgz && rm -f ${KAFKA}.tgz && ln -s ${KAFKA} kafka

ENV PATH=$PATH:/opt/kafka/bin

RUN apt-get clean

CMD ["bash"]
