FROM orchardup/python:2.7
RUN sed -i -e 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y wget git-core libpq-dev
WORKDIR /tmp
RUN wget https://github.com/maxmind/libmaxminddb/releases/download/0.5.6/libmaxminddb-0.5.6.tar.gz; tar xf libmaxminddb-0.5.6.tar.gz
RUN cd libmaxminddb-0.5.6; ./configure; make; sudo make install; sudo ldconfig
