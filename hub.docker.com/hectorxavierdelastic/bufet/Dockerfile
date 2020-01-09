FROM alpine:3.7

ENV DST=/home/
ENV URL=https://github.com/diwis/BUFET/archive/

RUN wget $URL/master.zip
RUN unzip master -d $DST/
RUN rm master.zip
RUN cd  $DST/BUFET-master

WORKDIR /BUFET-master/
