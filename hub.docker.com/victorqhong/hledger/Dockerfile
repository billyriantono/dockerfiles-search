FROM ubuntu:16.04

RUN apt-get update -y && \
    apt-get install -y hledger hledger-web && \
    apt-get clean

CMD ["hledger-web", "--server"]
