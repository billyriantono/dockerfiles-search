FROM kernsuite/base:dev
RUN docker-apt-install git python-presto presto python-numpy
#RUN git clone https://github.com/gajjarv/PulsarSearch /code
RUN git clone https://github.com/gijzelaerr/PulsarSearch /code
WORKDIR /code
RUN git checkout deb_pack_support

