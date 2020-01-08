FROM elasticsearch:5.6.3

MAINTAINER Xiao Ling

COPY /elasticsearch-analysis-ik-5.6.3.zip /home/elasticsearch-analysis-ik-5.6.3.zip
COPY /analysis-ik /usr/share/elasticsearch/config/analysis-ik

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install file:///home/elasticsearch-analysis-ik-5.6.3.zip && rm /home/elasticsearch-analysis-ik-5.6.3.zip && bin/elasticsearch-plugin install --batch x-pack
