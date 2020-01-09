FROM ubuntu
RUN apt-get update
RUN apt-get install qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools \
    build-essential libboost-all-dev libssl1.0-dev libdb++-dev libminiupnpc-dev git pwgen  -y
RUN git clone https://github.com/rutanio-sys/rutanio-qt.git
WORKDIR /rutanio-qt/src
RUN make -f makefile.unix
RUN mkdir ~/.rutanio/
COPY start.sh start.sh
RUN chmod +x start.sh
ENTRYPOINT ["./start.sh"]
