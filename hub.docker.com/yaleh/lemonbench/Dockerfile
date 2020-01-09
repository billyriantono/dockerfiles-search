FROM ubuntu

RUN apt update && apt install -y curl bash wget
RUN wget -4 -O /usr/local/bin/LemonBench.sh https://ilemonrain.com/download/shell/LemonBench.sh
RUN chmod +x /usr/local/bin/LemonBench.sh
RUN /usr/local/bin/LemonBench.sh -h && \
    /usr/local/bin/LemonBench.sh -f && \
    /usr/local/bin/LemonBench.sh --spoofer && \
    dpkg -P gcc g++ make protobuf-compiler libpcap-dev libprotobuf-dev

ENTRYPOINT ["/usr/local/bin/LemonBench.sh"]
