FROM openjdk:8

RUN cd /tmp && wget https://ci.destroystokyo.com/job/PaperSpigot/lastSuccessfulBuild/artifact/paperclip.jar && \
    mkdir /paper && mv /tmp/paperclip.jar /paper/paperclip.jar
WORKDIR /paper
ADD start.sh /paper/start.sh
RUN chmod +x /paper/start.sh
ADD eph.sh /eph.sh
RUN chmod +x /eph.sh

VOLUME /paper

ENV PMEM=2G

CMD /paper/start.sh
