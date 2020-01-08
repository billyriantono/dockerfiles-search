FROM zhangzisu/dsdpd:latest

WORKDIR /opt

RUN git clone https://github.com/rofl0r/microsocks.git && \
    cd microsocks && \
    echo "CFLAGS += -O2" >config.mak && \
    make

COPY kcptun /opt/kcptun
COPY startup /opt/startup

ENV DSDP_ID=1
ENV DSDP_GW=1025
ENV DSDP_NAME=docker
ENV DSDP_PASS=pass
ENV DSDPD_FR=8080
ENV GH_TOKEN=none
ENV GH_GIST=none
ENV KCPTUN_KEY=666233

WORKDIR /tmp
CMD [ "/opt/startup/run.sh" ]
