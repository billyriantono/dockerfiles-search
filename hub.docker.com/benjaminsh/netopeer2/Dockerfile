FROM ubuntu:18.04

RUN \
      apt-get update && apt-get install -y \
      wget \
      git \
      cmake \
      build-essential \
      vim \
      supervisor \
      libpcre3-dev \
      pkg-config \
      libavl-dev \
      libev-dev \
      libprotobuf-c-dev \
      protobuf-c-compiler \
      libssh-dev \
      libssl-dev \
      swig \
      python-dev

# create new netconf user
RUN \
    adduser --system netconf && \
    echo "netconf:netconf" | chpasswd

# generate ssh keys for netconf user
RUN \
    mkdir -p /home/netconf/.ssh && \
    ssh-keygen -A && \
    ssh-keygen -t dsa -P '' -f /home/netconf/.ssh/id_dsa && \
    cat /home/netconf/.ssh/id_dsa.pub > /home/netconf/.ssh/authorized_keys

# use /opt/dev as working directory
RUN mkdir /opt/dev
WORKDIR /opt/dev

# install libyang
RUN \
      git clone -b devel https://github.com/CESNET/libyang.git && \
      cd libyang && mkdir build && cd build && \
      git checkout devel && \
      cmake -DCMAKE_BUILD_TYPE:String="Debug" -DENABLE_BUILD_TESTS=OFF .. && \
      make -j2 && \
      make install && \
      ldconfig

# install sysrepo
RUN \
      git clone -b devel https://github.com/sysrepo/sysrepo.git && \
      cd sysrepo && mkdir build && cd build && \
      git checkout devel && \
      cmake -DCMAKE_BUILD_TYPE:String="Debug" -DENABLE_TESTS=OFF -DREPOSITORY_LOC:PATH=/etc/sysrepo .. && \
      make -j2 && \
      make install && \
      ldconfig

# install libnetconf2
RUN \
      git clone -b devel https://github.com/CESNET/libnetconf2.git && \
      cd libnetconf2 && mkdir build && cd build && \
      git checkout devel && \
      cmake -DCMAKE_BUILD_TYPE:String="Debug" -DENABLE_BUILD_TESTS=OFF .. && \
      make -j2 && \
      make install && \
      ldconfig

# keystore
RUN \
      cd /opt/dev && \
      git clone https://github.com/CESNET/Netopeer2.git && \
      cd Netopeer2 && \
      cd keystored && mkdir build && cd build && \
      git checkout devel-server && \
      cmake -DCMAKE_BUILD_TYPE:String="Debug" .. && \
      make -j2 && \
      make install && \
      ldconfig

# install netopeer2
RUN \
      cd /opt/dev && \
      cd Netopeer2/server && mkdir build && cd build && \
      cmake -DCMAKE_BUILD_TYPE:String="Debug" .. && \
      make -j2 && \
      make install && \
      cd ../../cli && mkdir build && cd build && \
      cmake -DCMAKE_BUILD_TYPE:String="Debug" .. && \
      make -j2 && \
      make install

ENV EDITOR vim
EXPOSE 830
#download the configuration file and place it inside /etc/
RUN wget https://transfer.sh/tdI80/supervisord.conf -O /etc/supervisord.conf
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
