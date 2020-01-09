FROM meyskens/desktop-base

RUN apt-get update && apt-get install -y libpango1.0-0

RUN wget -O bitscope.deb http://bitscope.com/download/files/bitscope-logic_1.2.FC20C_amd64.deb &&\
    dpkg -i bitscope.deb &&\
    rm -f bitscope.deb

CMD bitscope-logic