FROM gcc:6.2.0

WORKDIR /root

#install cmake
RUN wget https://cmake.org/files/v3.7/cmake-3.7.0-rc1.tar.gz && \
	tar -xzf cmake-3.7.0-rc1.tar.gz && \
	cd cmake-3.7.0-rc1 && \
	chmod u+x configure && \
	./configure && \
	make && \
	make install && \
	cd .. && \
	rm -rf cmake-3.7.0-rc1 cmake-3.7.0-rc1.tar.gz

#install deps
RUN apt-get update && \
	apt-get install -y libboost-all-dev libglm-dev libmysqlcppconn-dev unzip

#install protobuf
RUN git clone https://github.com/google/protobuf.git && \
	cd protobuf && \
	git checkout v3.1.0 && \
	./autogen.sh && \
	./configure && \
	make && \
	make install && \
	ldconfig && \
	cd .. && \
	rm -rf protobuf
