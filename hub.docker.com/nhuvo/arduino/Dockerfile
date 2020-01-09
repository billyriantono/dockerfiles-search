FROM debian:stretch
MAINTAINER Nhu-Hoai Robert VO <nhuhoai.vo@franicflow.ch>

RUN apt-get update && apt-get install -y wget xz-utils bash
RUN wget https://downloads.arduino.cc/arduino-1.8.5-linux64.tar.xz && tar xf arduino-1.8.5-linux64.tar.xz && \
    mv arduino-1.8.5 /opt && mv /opt/arduino-1.8.5 /opt/arduino && rm arduino-1.8.5-linux64.tar.xz && \
    mkdir /root/.arduino15/libraries -p

ENV PATH="/opt/arduino:${PATH}"

CMD ["/bin/bash"]
