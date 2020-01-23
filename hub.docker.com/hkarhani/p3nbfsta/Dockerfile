FROM hkarhani/p3nbfs:latest

MAINTAINER Hassan El Karhani <hkarhani@gmail.com>

WORKDIR /root
RUN wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz 
RUN tar -xzf ta-lib-0.4.0-src.tar.gz && cd ta-lib/ && ./configure --prefix=/usr && make && make install 

WORKDIR /notebooks

RUN pip3 install ta-lib mpl_finance

EXPOSE 8888

CMD /bin/sh -c "/usr/bin/jupyter notebook --allow-root"
