FROM alpine:3.7

ENV DST=/home/
ENV URL=http://carolina.imis.athena-innovation.gr/diana_team/microtss/

RUN wget $URL/microTSS_v1.0.tar.gz -O $DST/microTSS_v1.0.tar.gz
RUN tar -xvf $DST/microTSS_v1.0.tar.gz -C $DST/
RUN rm $DST/microTSS_v1.0.tar.gz
RUN cd  $DST/microTSS_v1.0

WORKDIR /microTSS_v1.0/
