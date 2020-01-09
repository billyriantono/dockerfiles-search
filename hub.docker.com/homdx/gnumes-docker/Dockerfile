FROM fedora

RUN dnf install git make gcc cpp wget curl mc nano texinfo -y && mkdir /app

WORKDIR /app

RUN git clone https://gitlab.com/janneke/tinycc.git && cd tinycc && ./configure && make && make install

RUN touch /var/log/test

CMD tail -f /var/log/test
