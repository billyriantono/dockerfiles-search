FROM yandex/trusty

RUN apt-get install -yy openjdk-7-jdk maven && apt-get clean

# Fork with operations support. Operations needed for ephemeralsCount
RUN git clone https://github.com/Naishy/jmxtrans.git
RUN cd jmxtrans && mvn install

ADD run.sh /root/run.sh

VOLUME ["/etc/jmxtrans"]

CMD /root/run.sh
