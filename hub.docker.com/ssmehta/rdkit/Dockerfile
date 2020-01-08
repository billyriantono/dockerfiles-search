FROM ubuntu:trusty
MAINTAINER Sajjan Singh Mehta "sajjan.s.mehta@gmail.com"

# Set RDKit version
ENV RDKIT_VERSION Release_2016_03_3

# Set home directory
ENV HOME /root
WORKDIR /root

# Download dependencies
RUN sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
	apt-get update && \
	apt-get -y upgrade && \
	apt-get install -y build-essential software-properties-common && \
	apt-get install -y byobu curl git htop man unzip vim wget && \
	apt-get install -y cmake flex bison python-numpy python-dev sqlite3 libsqlite3-dev libboost-dev libboost-system-dev libboost-thread-dev libboost-serialization-dev libboost-python-dev libboost-regex-dev && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# Compile rdkit
ADD https://github.com/rdkit/rdkit/archive/$RDKIT_VERSION.tar.gz /root/
RUN tar xzvf $RDKIT_VERSION.tar.gz && \
	rm $RDKIT_VERSION.tar.gz

RUN cd /root/rdkit-$RDKIT_VERSION/External/INCHI-API && \
	./download-inchi.sh

RUN mkdir /root/rdkit-$RDKIT_VERSION/build && \
	cd /root/rdkit-$RDKIT_VERSION/build && \
	cmake -DRDK_BUILD_INCHI_SUPPORT=ON .. && \
	make && \
	make install

# Set environmental variables
ENV RDBASE /root/rdkit-$RDKIT_VERSION
ENV LD_LIBRARY_PATH $RDBASE/lib
ENV PYTHONPATH $PYTHONPATH:$RDBASE

# Set data volume
RUN mkdir /data
VOLUME /data

# Add scripts
COPY includes/docker_entrypoint.sh /root
RUN chmod +x /root/docker_entrypoint.sh

# Set entrypoint
ENTRYPOINT ["./docker_entrypoint.sh"]