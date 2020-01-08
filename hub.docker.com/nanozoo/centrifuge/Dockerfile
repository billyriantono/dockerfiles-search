FROM ubuntu:bionic
ENV VERSION v1.0.4-beta

RUN apt-get update --fix-missing && apt-get install -y \
                                        python3 \
                                        git \
                                        make \
                                        g++ \
                                        wget \
                                        procps \
                                        ncbi-blast+ && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone --branch $VERSION https://github.com/infphilo/centrifuge
#WORKDIR /centrifuge
#RUN make
#RUN make install prefix=/usr/local
#ENV PATH /centrifuge/:$PATH

RUN cd /centrifuge && make
ENV PATH /centrifuge/:$PATH

# filter ont read script
COPY filter-reads-ont.sh /bin/
RUN chmod +x /bin/filter-reads-ont.sh