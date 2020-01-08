FROM maven:3-jdk-8

ENV BASE_DIR="/opt"

RUN mkdir -p $BASE_DIR /root/.m2

WORKDIR $BASE_DIR

COPY init.sh .

RUN chmod +x init.sh

CMD ${BASE_DIR}/init.sh && tail -f /dev/null
