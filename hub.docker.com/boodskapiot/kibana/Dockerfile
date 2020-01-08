FROM boodskapiot/ubuntu:18.04.jdk13

MAINTAINER platform@boodskap.io

LABEL Remarks="Kibana preconfigured for Boodskap IoT Platform"

WORKDIR /

RUN sudo adduser --disabled-password --gecos ""  kibana

RUN wget https://artifacts.elastic.co/downloads/kibana/kibana-7.5.1-linux-x86_64.tar.gz
RUN tar -xzf kibana-7.5.1-linux-x86_64.tar.gz
RUN mv kibana-7.5.1-linux-x86_64/* /home/kibana/
RUN rm -rf kibana-7.5.1-linux-x86_64

COPY kibana/ /home/kibana/
COPY start-kibana.sh .

RUN chmod +x start-kibana.sh

EXPOSE 5601

CMD ["/start-kibana.sh"]
