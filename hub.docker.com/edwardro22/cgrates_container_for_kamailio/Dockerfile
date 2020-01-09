FROM debian:jessie
MAINTAINER Eduard Tamsa

USER root
#CGRateS ENVs
ENV GOROOT=/root/go
ENV GOPATH=/root/code
ENV PATH=$GOROOT/bin:$GOPATH/bin:$PATH

#RUN [ "sh", "-c", "export GOROOT=/root/go; export GOPATH=/root/code; export PATH=$GOROOT/bin:$GOPATH/bin:$PATH" ]

# set mysql password
RUN echo 'mysql-server mysql-server/root_password password CGRateS.org' | debconf-set-selections && echo 'mysql-server mysql-server/root_password_again password CGRateS.org' | debconf-set-selections

# install dependencies
RUN apt-get -y update && apt-get -y install autoconf build-essential openssl libssl-dev libsrtp-dev libxml2-dev libncurses5-dev uuid-dev sqlite3 libsqlite3-dev pkg-config ngrep libjansson-dev git python-pycurl python-mysqldb sudo wget 

# add cgrates user
RUN useradd -c CGRateS -d /var/run/cgrates -s /bin/false -r cgrates

# install golang
RUN wget -qO- https://storage.googleapis.com/golang/go1.9.linux-amd64.tar.gz | tar xzf - -C /root/

#install glide
RUN go get github.com/Masterminds/glide
RUN cd /root/code/src/github.com/  && \
    mkdir cgrates && cd cgrates && \
    git clone https://github.com/cgrates/cgrates.git && \
    cd cgrates && \
    ls && \
    glide install && \
    ./build.sh &&\
    ln -s /root/code/src/github.com/cgrates/cgrates/data /usr/share/cgrates


# cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# set start command
#CMD /root/code/src/github.com/cgrates/cgrates/data/docker/devel/start.sh
CMD export GOROOT=/root/go; export GOPATH=/root/code; export PATH=$GOROOT/bin:$GOPATH/bin:$PATH

COPY cgrates.json /cgrConfig/cgrates.json

COPY start.sh start/start.sh

#script taken from https://github.com/vishnubob/wait-for-it
COPY wait-for-it.sh wait-for-it.sh

ENTRYPOINT ["start/start.sh"]

