FROM debian:stretch

#########################
# Basics
#########################
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y mosquitto-clients supervisor libsrtp-dev libasound2-dev libpjmedia-codec2 wget mosquitto-clients

#RUN apt-get install -y python3 python3-pip 
#RUN  pip3 install paho-mqtt configparser

RUN apt-get install -y python python-pip 
RUN  pip install paho-mqtt configparser

COPY config/etc /etc
COPY config/pjsua_call.patch /tmp
COPY config/mqtt2sip.ini /usr/local/bin
COPY config/mqtt2sip.py  /usr/local/bin
COPY config/triggerTestCall /usr/local/bin

#########################
## sipcmd - funktioniert nicht mehr richtig, legt nicht auf - komischer fehler, scheint abzubrechen ohne die verbindungen zu killen
#########################
#RUN cd /tmp ; git clone https://github.com/tmakkonen/sipcmd.git ; cd sipcmd; make;

#########################
# python self compiled
# http://most-voip.readthedocs.io/en/latest/python_docs/tutorial/voip_tutorial_1.html#step-1-initialize-the-library
#########################
ENV PJVERS 2.8
ENV PJPATH /tmp/pjsip

RUN mkdir -p $PJPATH

RUN cd $PJPATH && wget http://www.pjsip.org/release/${PJVERS}/pjproject-${PJVERS}.tar.bz2 && \
    tar -jxvf pjproject-${PJVERS}.tar.bz2

WORKDIR ${PJPATH}/pjproject-${PJVERS}
RUN ./configure --enable-shared	 

## Compile issues.. Created a small patch, not sure about the impact. Compile & call works now
#########################
RUN patch --ignore-whitespace ${PJPATH}/pjproject-${PJVERS}/pjsip/src/pjsua-lib/pjsua_call.c /tmp/pjsua_call.patch 

RUN make dep && make && make install 
RUN cd ${PJPATH}/pjproject-${PJVERS}/pjsip-apps/src/python && python setup.py install

RUN echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib" >> /root/.bashrc

WORKDIR /usr/local/bin
CMD rm -rf /etc/localtime; ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime ; /etc/init.d/supervisor start && tail -f /dev/null
