FROM debian:jessie

RUN apt-get update && apt-get install -y default-jre-headless jsvc wget
RUN wget  wget http://dl.ubnt.com/crmpoint/package/crmpoint_0.3.5_amd64.deb &&\
    dpkg -i crmpoint_0.3.5_amd64.deb &&\
    rm crmpoint_0.3.5_amd64.deb && \ 
    apt-get install -fy


ENTRYPOINT service crmpoint start && tail -f /usr/share/crmpoint/logs/*
