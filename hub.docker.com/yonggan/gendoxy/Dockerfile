FROM debian:latest

RUN apt update && apt install -y python3 python3-pip git graphviz g++ python cmake flex bison

RUN git clone https://github.com/doxygen/doxygen.git /data/doxygen/install
RUN mkdir -p /data/doxygen
RUN mkdir -p /data/doxygen/output
RUN mkdir -p /data/doxygen/install/build
RUN cd /data/doxygen/install/build && cmake -G "Unix Makefiles" .. && make && make install
RUN rm -rf /data/doxygen/install
COPY start.sh /data
COPY Doxyfile /data/doxygen
COPY styles.css /data/doxygen
WORKDIR /data
VOLUME ["/data"]