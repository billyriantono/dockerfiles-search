FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.5
MAINTAINER Patrick Laurin <plaurin@inocybe.ca>
USER root
RUN wget https://packages.elastic.co/curator/5/centos/7/Packages/elasticsearch-curator-5.4.1-1.x86_64.rpm
RUN rpm -ivh elasticsearch-curator-5.4.1-1.x86_64.rpm
RUN rm elasticsearch-curator-5.4.1-1.x86_64.rpm
RUN elasticsearch-plugin remove x-pack
USER elasticsearch
# Below locale envs required for curator cli to work 
ENV LC_ALL=en_US.utf-8
ENV LANG=en_US.utf-8
