FROM debian:stretch

RUN apt-get update && \
    apt-get install -y \
      wget \
      zip;

RUN wget https://github.com/tkuchiki/alp/releases/download/v0.3.1/alp_linux_amd64.zip && \
    unzip alp_linux_amd64.zip && \
    mv alp /usr/local/bin && \
    rm alp_linux_amd64.zip

RUN mkdir /logs
WORKDIR /logs

ENTRYPOINT ["alp"]
CMD ["-f", "access.log"]
