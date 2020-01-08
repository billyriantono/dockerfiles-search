FROM opensuse/tumbleweed
WORKDIR /root
RUN zypper -n update && zypper -n install tar gzip java-12-openjdk && zypper clean -a
COPY archive/kafka_2.12-2.3.0.tgz .
RUN mkdir -p /kafka && tar zxvf kafka_2.12-2.3.0.tgz && mv kafka_2.12-2.3.0/* /kafka && rm -rf *
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
EXPOSE 9092
ENTRYPOINT ["/docker-entrypoint.sh"]
