# Dockerfile for ELK stack

# Build with:
# docker build -t thaicyber/elk-632-icu .

# TEST
# sudo docker run --ulimit nofile=90000:90000 -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk_632_icu thaicyber/elk_632_icu
# sudo docker run --ulimit nofile=90000:90000 -p 5601:5601 -p 9200:9200 -p 9300:9300 -p 5044:5044 -dit --restart unless-stopped --name elk-632-icu thaicyber/elk-632-icu

FROM sebp/elk:632

ENV ES_HOME /opt/elasticsearch
WORKDIR ${ES_HOME}

RUN yes | CONF_DIR=/etc/elasticsearch gosu elasticsearch bin/elasticsearch-plugin \
    install -b analysis-icu